# 🚀 Quick Start Guide

Get started with GitHub Actions Learning in 5 minutes!

## Prerequisites

- GitHub account
- Node.js 16+ installed locally
- Basic Git knowledge

## Step 1: Clone the Repository

```bash
git clone https://github.com/YOUR-USERNAME/github-actions-learning.git
cd github-actions-learning
```

## Step 2: Set Up the Sample App

```bash
cd sample-app
npm install
npm start
```

Visit `http://localhost:3000` - You should see a welcome message!

## Step 3: Run Tests

```bash
npm test
```

All tests should pass ✅

## Step 4: Explore Workflows

Go to your repository on GitHub:
1. Click the **Actions** tab
2. You'll see workflows ready to run:
   - **Hello World Workflow** - Try manual trigger
   - **Build and Test** - Runs on push
   - **Deploy to Azure** - Deployment example

## Step 5: Read the Learning Path

Start with the documentation in order:

1. [What is GitHub Actions?](docs/01-what-is-github-actions.md) - 10 min
2. [Workflow Basics](docs/02-workflow-basics.md) - 15 min
3. [Triggers and Events](docs/03-triggers-and-events.md) - 10 min
4. [Jobs and Steps](docs/04-jobs-and-steps.md) - 15 min
5. [Secrets and Environment Variables](docs/05-secrets-and-env.md) - 10 min
6. [Build and Test](docs/06-build-and-test.md) - 15 min
7. [Deploy to Azure](docs/07-deploy-to-azure.md) - 10 min

## Step 6: Try the Tasks

Complete hands-on exercises in [TASKS.md](TASKS.md):

- **Beginner:** Tasks 1-3 (30 min)
- **Intermediate:** Tasks 4-7 (1-2 hours)
- **Advanced:** Tasks 8-10 (2-3 hours)

## 🎯 Next Steps

1. **Create an Issue** - Use templates in `.github/ISSUE_TEMPLATE/`
2. **Fork & Contribute** - See [CONTRIBUTING.md](CONTRIBUTING.md)
3. **Deploy to Azure** - Challenge task in [TASKS.md](TASKS.md)
4. **Build Your Own** - Apply to your projects!

## 📁 Repository Structure

```
github-actions-learning/
├── 📖 docs/                      # Complete learning guides
├── 🔧 .github/
│   ├── workflows/               # Example workflows
│   └── ISSUE_TEMPLATE/         # Contribution templates
├── 🎯 sample-app/              # Example Node.js app
├── 📝 TASKS.md                 # Hands-on exercises
├── 📚 README.md                # Main guide
└── 🤝 CONTRIBUTING.md          # How to contribute
```

## ⚡ Common Commands

```bash
# Run sample app
cd sample-app && npm start

# Run tests
cd sample-app && npm test

# Run linting
cd sample-app && npm run lint

# View workflows
# (In browser: GitHub Actions tab)
```

## 🆘 Troubleshooting

### Port 3000 Already in Use
```bash
npm start -- --port 3001
```

### Tests Failing
```bash
cd sample-app
npm install  # Reinstall dependencies
npm test
```

### Workflow Not Running
1. Check Actions tab for errors
2. Verify you pushed to `main` or `develop` branch
3. Check `.github/workflows/*.yml` syntax

## 📖 Learning Resources

- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [GitHub Actions Marketplace](https://github.com/marketplace?type=actions)
- [Azure Documentation](https://docs.microsoft.com/en-us/azure/)

## 💡 Tips for Success

✅ Read one doc section at a time  
✅ Try the tasks as you learn  
✅ Modify workflows to experiment  
✅ Check logs when something fails  
✅ Ask questions in Issues tab  

## 🎓 Learning Outcomes

After completing this course, you'll understand:

- ✅ How GitHub Actions works
- ✅ Creating and managing workflows
- ✅ Building CI/CD pipelines
- ✅ Running tests automatically
- ✅ Deploying to Azure
- ✅ Using secrets securely
- ✅ Working with job dependencies
- ✅ Matrix testing and parallel jobs

## 🌟 Show Your Support

- ⭐ Star this repository
- 🔄 Share with others
- 🐛 Report issues
- 💡 Suggest improvements
- 🤝 Contribute enhancements

---

**Ready? Let's go! Start with [docs/01-what-is-github-actions.md](docs/01-what-is-github-actions.md) 🚀**
