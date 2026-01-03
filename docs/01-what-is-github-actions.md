# What is GitHub Actions?

## Overview

**GitHub Actions** is a continuous integration and continuous deployment (CI/CD) platform that allows you to automate your build, test, and deployment pipeline. GitHub Actions runs your workflows when specific events happen in your repository.

## Key Concepts

### What Can You Do?

- **Automate Testing:** Run tests automatically on every push
- **Build Applications:** Compile and package your code
- **Deploy Code:** Push to production automatically
- **Create Releases:** Generate release notes and packages
- **Send Notifications:** Alert teams of important events
- **Run Scheduled Tasks:** Execute workflows on a schedule

### Why Use GitHub Actions?

✅ **No Extra Tools Needed** - Built directly into GitHub  
✅ **Free for Public Repos** - Generous free tier  
✅ **Easy Setup** - Simple YAML configuration  
✅ **Integrated with GitHub** - Works seamlessly with your repo  
✅ **Community Actions** - Use pre-built actions from the marketplace  
✅ **Flexible** - Run on GitHub-hosted or self-hosted runners  

## Core Components

### 1. Workflows
A workflow is an automated procedure that runs jobs. It's defined in a YAML file in `.github/workflows/` directory.

### 2. Events
Events are specific activities that trigger a workflow run:
- Push to repository
- Pull request creation
- Release published
- Scheduled time (cron)
- Manual trigger
- And many more...

### 3. Jobs
A job is a set of steps that run in the same runner. Jobs run in parallel by default unless you specify dependencies.

### 4. Steps
A step is an individual task that can run commands or call an action.

### 5. Actions
Actions are standalone commands that can be combined into steps. You can create your own or use community actions.

### 6. Runners
A runner is a server that runs your workflow. GitHub provides hosted runners, or you can use self-hosted runners.

## Basic Workflow Example

```yaml
name: My First Workflow
on: push

jobs:
  hello-world:
    runs-on: ubuntu-latest
    steps:
      - name: Print hello
        run: echo "Hello, World!"
```

**What happens:**
1. Workflow is triggered on every push
2. A job called `hello-world` runs
3. It runs on an Ubuntu machine
4. It executes one step: printing "Hello, World!"

## Workflow Execution Flow

```
Event Triggered (e.g., push)
        ↓
Workflow Starts
        ↓
Jobs Run (can run in parallel)
        ↓
Steps Execute (run sequentially in each job)
        ↓
Actions Execute (individual tasks)
        ↓
Workflow Complete
```

## When Should You Use GitHub Actions?

| Use Case | Example |
|----------|---------|
| **Testing** | Run unit tests on every PR |
| **Building** | Compile code and create artifacts |
| **Deployment** | Deploy to servers or cloud platforms |
| **Publishing** | Release packages to npm, PyPI, etc. |
| **Notifications** | Send Slack messages on failures |
| **Code Quality** | Run linters and security scans |
| **Scheduling** | Backup data daily, clean up old files |

## Pricing

- **Public Repositories:** Unlimited free usage
- **Private Repositories:** 2,000 minutes/month free, then paid
- **Self-hosted Runners:** No usage limits

## Next Steps

Ready to learn more? Check out:
- [Workflow Basics](02-workflow-basics.md)
- [Triggers and Events](03-triggers-and-events.md)
- [GitHub Actions Documentation](https://docs.github.com/en/actions)

## Quick Recap

✅ GitHub Actions automates tasks triggered by events  
✅ Workflows are YAML files that define automation  
✅ Free to use on public repositories  
✅ Integrates seamlessly with GitHub  
✅ Powerful for CI/CD and automation  

---

**Ready to create your first workflow? Let's go to the next lesson!**
