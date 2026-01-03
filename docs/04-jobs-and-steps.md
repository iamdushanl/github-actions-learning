# Jobs and Steps

## Deep Dive: Jobs

A **job** is a collection of steps that execute on the same runner. Think of a job as a unit of work.

## Job Configuration

### Basic Job

```yaml
jobs:
  my-job:
    runs-on: ubuntu-latest
    steps:
      - run: echo "Hello"
```

### Complete Job Configuration

```yaml
jobs:
  my-job:
    name: My Custom Job Name
    runs-on: ubuntu-latest
    needs: [other-job]
    if: success()
    environment: production
    concurrency: my-group
    timeout-minutes: 30
    strategy:
      matrix:
        node-version: [14, 16, 18]
    steps:
      - run: echo "Running"
```

## Job Properties

| Property | Type | Description |
|----------|------|-------------|
| `runs-on` | string/array | Runner to use |
| `name` | string | Job display name |
| `needs` | string/array | Jobs that must complete first |
| `if` | string | Conditional expression |
| `environment` | string/object | Environment configuration |
| `concurrency` | string/object | Concurrency limits |
| `timeout-minutes` | number | Max execution time |
| `strategy` | object | Matrix and fail-fast settings |
| `steps` | array | Job steps |

## Running Jobs in Parallel

By default, jobs run **in parallel**:

```yaml
jobs:
  job-one:
    runs-on: ubuntu-latest
    steps:
      - run: echo "Job 1"
      - run: sleep 30

  job-two:
    runs-on: ubuntu-latest
    steps:
      - run: echo "Job 2"
```

**Timeline:**
- 0s: Both jobs start simultaneously
- 30s: Job 1 finishes, Job 2 finishes

## Job Dependencies

Make jobs run **sequentially** using `needs`:

```yaml
jobs:
  setup:
    runs-on: ubuntu-latest
    steps:
      - run: echo "Setting up..."

  test:
    needs: setup
    runs-on: ubuntu-latest
    steps:
      - run: echo "Running tests..."

  deploy:
    needs: test
    runs-on: ubuntu-latest
    steps:
      - run: echo "Deploying..."
```

**Timeline:**
- setup → test → deploy

Multiple dependencies:

```yaml
deploy:
  needs: [test, lint]  # Waits for both
  runs-on: ubuntu-latest
  steps:
    - run: echo "Deploy"
```

## Conditional Execution

### Using `if`

```yaml
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - run: npm test

  deploy:
    needs: test
    if: github.ref == 'refs/heads/main'
    runs-on: ubuntu-latest
    steps:
      - run: echo "Deploying"
```

### Common Conditions

```yaml
if: success()              # Previous job succeeded
if: failure()              # Previous job failed
if: always()               # Always run, regardless
if: github.event_name == 'push'  # Check event type
if: contains(github.actor, 'bot')  # Check actor
if: github.repository == 'owner/repo'  # Check repo
```

## Matrix Strategy

Run a job with multiple configurations:

```yaml
jobs:
  test:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        node-version: [14, 16, 18]
        os: [ubuntu-latest, macos-latest]
    steps:
      - uses: actions/setup-node@v3
        with:
          node-version: ${{ matrix.node-version }}
      - run: npm test
```

This creates **6 jobs** (3 node versions × 2 OSes), all running in parallel!

### Matrix Context

```yaml
${{ matrix.node-version }}  # Access matrix variables
${{ matrix.os }}
```

### Include/Exclude

```yaml
strategy:
  matrix:
    node-version: [14, 16, 18]
    include:
      - node-version: 18
        experimental: true
    exclude:
      - node-version: 14
        os: macos-latest
```

## Fail-Fast

Stop all jobs if one fails:

```yaml
strategy:
  fail-fast: true
  matrix:
    node-version: [14, 16, 18]
```

Or allow others to continue:

```yaml
strategy:
  fail-fast: false
  matrix:
    node-version: [14, 16, 18]
```

## Deep Dive: Steps

A **step** is a single task within a job.

### Step Types

#### 1. Run Shell Command

```yaml
steps:
  - run: npm install
  - run: npm test
```

Multiple lines:

```yaml
- run: |
    npm install
    npm test
    npm build
```

#### 2. Use an Action

```yaml
steps:
  - uses: actions/checkout@v3
```

With parameters:

```yaml
- uses: actions/setup-node@v3
  with:
    node-version: '18'
    cache: 'npm'
```

#### 3. Shell Selection

```yaml
- run: echo "Hello"
  shell: bash

- run: 'echo "Hello"'
  shell: powershell  # Windows
```

## Step Properties

```yaml
steps:
  - name: Install dependencies
    run: npm install
    working-directory: ./src
    env:
      NODE_ENV: development
    if: success()
    timeout-minutes: 10
    continue-on-error: false
```

| Property | Description |
|----------|-------------|
| `name` | Step display name |
| `run` | Command to run |
| `uses` | Action to use |
| `with` | Action inputs |
| `env` | Environment variables |
| `if` | Conditional execution |
| `timeout-minutes` | Max execution time |
| `continue-on-error` | Don't fail job on error |
| `working-directory` | Working directory |
| `shell` | Shell type (bash, powershell) |

## Environment Variables

Set per-step:

```yaml
- run: npm install
  env:
    NODE_ENV: production
    DEBUG: true
```

Set for entire job:

```yaml
env:
  NODE_ENV: production

jobs:
  test:
    runs-on: ubuntu-latest
    env:
      VERSION: 1.0.0
    steps:
      - run: echo $VERSION
```

## Continue on Error

Continue running even if a step fails:

```yaml
- run: npm run lint
  continue-on-error: true
```

## Step Outputs

Pass data between steps:

```yaml
- id: get-version
  run: echo "version=1.0.0" >> $GITHUB_OUTPUT

- run: echo "Version is ${{ steps.get-version.outputs.version }}"
```

## Real-World Example

```yaml
name: Node.js CI

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  test:
    name: Test on Node ${{ matrix.node-version }}
    runs-on: ubuntu-latest
    
    strategy:
      matrix:
        node-version: [14, 16, 18]
    
    steps:
      - name: Checkout code
        uses: actions/checkout@v3
      
      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: ${{ matrix.node-version }}
          cache: 'npm'
      
      - name: Install dependencies
        run: npm ci
      
      - name: Run linter
        run: npm run lint
        continue-on-error: true
      
      - name: Run tests
        run: npm test
        if: success()
      
      - name: Upload coverage
        uses: codecov/codecov-action@v3
        if: always()
```

## Best Practices

✅ Use **descriptive step names**  
✅ Use **actions** instead of shell scripts when possible  
✅ Use **matrix** for testing multiple configurations  
✅ **Cache dependencies** to speed up runs  
✅ Use **continue-on-error** for non-critical steps  
✅ **Check out code** early in your steps  

## Common Mistakes

❌ Forgetting to checkout code  
❌ Not using step names (hard to debug)  
❌ Making jobs too dependent (slow runs)  
❌ Not caching dependencies (slow and wasteful)  
❌ Running too many matrix combinations  

## Next Steps

- [Secrets and Environment Variables](05-secrets-and-env.md) - Secure your workflows
- [Build and Test](06-build-and-test.md) - Real-world examples
- [Deploy to Azure](07-deploy-to-azure.md) - Cloud deployment

---

**You now understand jobs and steps! Next, let's secure your workflows with secrets.**
