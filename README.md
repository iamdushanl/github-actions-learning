# 🚀 GitHub Actions Learning Repository

Welcome to your hands-on learning journey with **GitHub Actions**! This repository is designed for beginners and intermediate developers who want to master CI/CD automation.

## 📚 What You'll Learn

- ✅ GitHub Actions fundamentals (workflows, jobs, steps)
- ✅ Automating builds and tests
- ✅ CI/CD pipeline creation
- ✅ Deploying applications to Azure App Service
- ✅ Working with secrets and environment variables
- ✅ Real-world workflow examples

## 🎯 Target Audience

- Beginners to CI/CD
- Developers wanting to automate their workflows
- Students learning DevOps practices
- Anyone interested in GitHub Actions

## 📋 Prerequisites

Before starting, make sure you have:

- A GitHub account
- Basic Git knowledge
- Node.js installed (v16 or higher) for running sample apps
- (Optional) Azure account for deployment workflows

## 🗂️ Repository Structure

```
github-actions-learning/
├── README.md                          # You are here!
├── docs/                              # Learning documentation
│   ├── 01-what-is-github-actions.md
│   ├── 02-workflow-basics.md
│   ├── 03-triggers-and-events.md
│   ├── 04-jobs-and-steps.md
│   ├── 05-secrets-and-env.md
│   ├── 06-build-and-test.md
│   └── 07-deploy-to-azure.md
├── .github/
│   ├── workflows/                     # Example workflows
│   │   ├── hello-world.yml
│   │   ├── build-test.yml
│   │   └── deploy-azure-app-service.yml
│   ├── ISSUE_TEMPLATE/                # Issue templates
│   └── PULL_REQUEST_TEMPLATE.md       # PR template
├── sample-app/                        # Sample Node.js application
│   ├── src/
│   ├── tests/
│   ├── package.json
│   └── README.md
├── TASKS.md                           # Hands-on exercises
└── assets/                            # Images and diagrams
```

## 🚦 Getting Started

### 1. Clone this Repository

```bash
git clone https://github.com/YOUR-USERNAME/github-actions-learning.git
cd github-actions-learning
```

### 2. Follow the Learning Path

Start with the documentation in order:

1. [What is GitHub Actions?](docs/01-what-is-github-actions.md)
2. [Workflow Basics](docs/02-workflow-basics.md)
3. [Triggers and Events](docs/03-triggers-and-events.md)
4. [Jobs and Steps](docs/04-jobs-and-steps.md)
5. [Secrets and Environment Variables](docs/05-secrets-and-env.md)
6. [Build and Test](docs/06-build-and-test.md)
7. [Deploy to Azure](docs/07-deploy-to-azure.md)

### 3. Try the Sample App

```bash
cd sample-app
npm install
npm start
```

Visit `http://localhost:3000` to see the app running.

### 4. Complete the Tasks

Check [TASKS.md](TASKS.md) for hands-on exercises to practice what you've learned.

## 🔧 Example Workflows

This repository includes three practical workflows:

### 1. Hello World Workflow
**File:** [.github/workflows/hello-world.yml](.github/workflows/hello-world.yml)
- Triggers on push
- Prints messages
- Perfect for understanding basics

### 2. Build & Test Workflow
**File:** [.github/workflows/build-test.yml](.github/workflows/build-test.yml)
- Installs dependencies
- Runs tests
- Checks code quality

### 3. Deploy to Azure App Service
**File:** [.github/workflows/deploy-azure-app-service.yml](.github/workflows/deploy-azure-app-service.yml)
- Builds the application
- Deploys to Azure App Service
- Uses GitHub Secrets for credentials

## 🎓 Learning Tips

1. **Start Small:** Begin with the hello-world workflow
2. **Experiment:** Modify workflows and see what happens
3. **Read Logs:** GitHub Actions logs are your best friend
4. **Use Issues:** Practice with our issue templates
5. **Make PRs:** Fork this repo and create pull requests

## 🤝 Contributing

We welcome contributions! To contribute:

1. Fork this repository
2. Create a new branch (`git checkout -b feature/your-feature`)
3. Make your changes
4. Commit your changes (`git commit -m 'Add some feature'`)
5. Push to the branch (`git push origin feature/your-feature`)
6. Open a Pull Request using our [PR template](.github/PULL_REQUEST_TEMPLATE.md)

## 📝 Reporting Issues

Found a bug or have a suggestion? Use our issue templates:

- 🐛 [Bug Report](.github/ISSUE_TEMPLATE/bug_report.md)
- ✨ [Feature Request](.github/ISSUE_TEMPLATE/feature_request.md)
- 📚 [Documentation Issue](.github/ISSUE_TEMPLATE/documentation.md)
- ❓ [Question](.github/ISSUE_TEMPLATE/question.md)

## 🏆 Challenge Yourself

- [ ] Complete all tasks in [TASKS.md](TASKS.md)
- [ ] Create your own custom workflow
- [ ] Deploy the sample app to Azure
- [ ] Add a new feature to the sample app with CI/CD
- [ ] Help others by answering questions in Issues

## 📚 Additional Resources

- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [GitHub Actions Marketplace](https://github.com/marketplace?type=actions)
- [Azure App Service Documentation](https://docs.microsoft.com/en-us/azure/app-service/)

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🌟 Show Your Support

If you find this repository helpful, please give it a ⭐️ and share it with others!

---

**Happy Learning! 🎉**

For questions or feedback, feel free to open an issue or reach out to the community.
