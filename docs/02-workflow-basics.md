# Workflow Basics

## What is a Workflow?

A **workflow** is an automated process defined in a YAML file that GitHub Actions executes. It contains all the instructions for what should happen when triggered.

## Workflow File Location

Workflow files must be placed in:
```
.github/workflows/
```

All files should be `.yml` or `.yaml` format.

## Basic Workflow Structure

```yaml
name: My Workflow

on: push

jobs:
  my-job:
    runs-on: ubuntu-latest
    steps:
      - name: My Step
        run: echo "Hello!"
```

## Required Components

### 1. Name
The name of your workflow (displayed in GitHub UI):
```yaml
name: Build and Test
```

### 2. On (Trigger)
When should this workflow run? See [Triggers and Events](03-triggers-and-events.md) for details:
```yaml
on: push
```

### 3. Jobs
Contains one or more jobs that will run:
```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      # steps here
```

## Jobs Explained

A job is a collection of steps that run on the **same runner** (machine).

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - run: npm install
      - run: npm test
      - run: npm build
```

### Job Properties

| Property | Description |
|----------|-------------|
| `runs-on` | The type of machine to run on |
| `steps` | Array of steps to execute |
| `needs` | Job dependencies (other jobs that must complete first) |
| `if` | Conditional execution |
| `strategy` | Matrix strategy for multiple configurations |
| `environment` | Environment name for this job |

## Steps Explained

A step is a single action in a job. Steps run **sequentially** on the same runner.

### Types of Steps

#### 1. Run Command
```yaml
- run: echo "Hello World"
```

#### 2. Use an Action
```yaml
- uses: actions/checkout@v3
```

#### 3. Named Step
```yaml
- name: Check out code
  uses: actions/checkout@v3
```

## Step Properties

```yaml
steps:
  - name: Install dependencies
    run: npm install
    working-directory: ./app
    shell: bash
    if: success()
```

| Property | Description |
|----------|-------------|
| `name` | Human-readable name (displayed in logs) |
| `run` | Command line program to run |
| `uses` | Action to use (from marketplace or local) |
| `with` | Input parameters for actions |
| `env` | Environment variables |
| `if` | Conditional execution |
| `working-directory` | Working directory for this step |

## Running Multiple Jobs

Jobs run **in parallel** by default:

```yaml
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - run: npm test

  lint:
    runs-on: ubuntu-latest
    steps:
      - run: npm run lint
```

Both `test` and `lint` run at the same time!

## Job Dependencies (Sequential Jobs)

Make one job wait for another:

```yaml
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - run: npm test

  deploy:
    needs: test  # Wait for 'test' job to complete
    runs-on: ubuntu-latest
    steps:
      - run: npm run deploy
```

Now `deploy` only runs **after** `test` completes successfully.

## Runners

A runner is a server that executes your jobs.

### GitHub-Hosted Runners

```yaml
runs-on: ubuntu-latest    # Linux
runs-on: macos-latest     # macOS
runs-on: windows-latest   # Windows
```

### Available Runners

| Runner | OS | Pre-installed Tools |
|--------|----|--------------------|
| `ubuntu-latest` | Ubuntu 22.04 | Node, Python, Go, Ruby, Docker |
| `macos-latest` | macOS 13 | Xcode, Node, Python, Ruby |
| `windows-latest` | Windows Server 2022 | Visual Studio, Node, Python |

## Example: Complete Workflow

```yaml
name: Build, Test, and Deploy

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  build:
    name: Build Application
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'

      - name: Install dependencies
        run: npm install

      - name: Build app
        run: npm run build

  test:
    name: Run Tests
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'

      - name: Install dependencies
        run: npm install

      - name: Run tests
        run: npm test

  deploy:
    name: Deploy to Production
    runs-on: ubuntu-latest
    needs: test
    if: github.ref == 'refs/heads/main'
    steps:
      - name: Deploy
        run: echo "Deploying to production..."
```

**Execution Flow:**
1. `build` and `test` are triggered
2. `test` waits for `build` to complete
3. `deploy` only runs if `test` succeeds AND we're on main branch

## Best Practices

✅ Use **clear, descriptive names** for workflows and steps  
✅ Use **actions from the marketplace** instead of custom scripts  
✅ **Cache dependencies** to speed up workflows  
✅ **Use conditions** to prevent unnecessary runs  
✅ **Set timeouts** to prevent hung workflows  
✅ Keep workflows **simple and focused**  

## Common Mistakes

❌ Not checking out code with `actions/checkout`  
❌ Using `run` instead of `uses` for actions  
❌ Forgetting to set required `with` parameters  
❌ Making jobs dependent when they should run in parallel  
❌ Not using failure conditions properly  

## Next Steps

- [Triggers and Events](03-triggers-and-events.md) - Learn what events trigger workflows
- [Jobs and Steps](04-jobs-and-steps.md) - Deep dive into jobs and steps
- [Secrets and Environment Variables](05-secrets-and-env.md) - Manage sensitive data

---

**You now understand workflow basics! Ready to learn about triggers?**
