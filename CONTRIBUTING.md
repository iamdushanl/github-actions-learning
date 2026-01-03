# Contributing to GitHub Actions Learning

Thank you for your interest in contributing! This document provides guidelines for contributing to this project.

## 🎯 Our Mission

We aim to provide the best hands-on learning resources for GitHub Actions. Your contributions help us achieve this goal!

## ✨ How to Contribute

### 1. Report Bugs
Found a bug? Please create an issue using the [bug report template](.github/ISSUE_TEMPLATE/bug_report.md).

Include:
- What you were doing
- What happened
- What you expected to happen
- Your environment (OS, Node version, etc.)

### 2. Suggest Features
Have an idea to improve this learning resource? Create an issue using the [feature request template](.github/ISSUE_TEMPLATE/feature_request.md).

Include:
- Clear description of the feature
- Why it would be useful for learning
- Example use case

### 3. Improve Documentation
Documentation unclear or missing? Create an issue using the [documentation template](.github/ISSUE_TEMPLATE/documentation.md).

### 4. Submit Code Changes

#### Fork and Clone
```bash
git clone https://github.com/YOUR-USERNAME/github-actions-learning.git
cd github-actions-learning
```

#### Create a Branch
```bash
git checkout -b feature/your-feature-name
```

Branch naming convention:
- `feature/description` - New features
- `fix/description` - Bug fixes
- `docs/description` - Documentation updates
- `test/description` - Adding tests

#### Make Changes
1. Make your changes
2. Test locally: `npm test` in the `sample-app` directory
3. Follow the code style

#### Commit Changes
```bash
git commit -m "Clear, descriptive commit message"
```

Commit message format:
- Use imperative mood ("Add feature" not "Added feature")
- Keep it short (50 chars or less)
- Reference issues when relevant: "Fix #123"

#### Push and Create PR
```bash
git push origin feature/your-feature-name
```

Create a Pull Request on GitHub using the [PR template](.github/PULL_REQUEST_TEMPLATE.md).

## 📋 PR Guidelines

Your PR should:
- [ ] Have a clear title and description
- [ ] Reference any related issues
- [ ] Include tests for new features
- [ ] Update documentation if needed
- [ ] Pass all CI/CD checks
- [ ] Fit the project's learning goals

## 🏗️ Project Structure

```
github-actions-learning/
├── docs/                  # Learning documentation
├── sample-app/           # Example Node.js application
├── .github/
│   ├── workflows/        # GitHub Actions workflows
│   └── ISSUE_TEMPLATE/   # Issue templates
├── TASKS.md             # Learning exercises
└── README.md            # Main guide
```

## 📝 Code Style

### JavaScript
- Use 2-space indentation
- Use `const`/`let` (not `var`)
- Add comments for complex logic
- Use meaningful variable names

### YAML (Workflows)
- Use 2-space indentation
- Use descriptive step names
- Comment non-obvious configurations
- Test workflows before submitting

### Markdown
- Use clear, concise language
- Add code examples where appropriate
- Link to relevant documentation
- Check spelling and grammar

## 🧪 Testing

Before submitting:

```bash
cd sample-app
npm install
npm test
npm run lint
npm start  # Test manually
```

All tests must pass!

## 📚 Documentation

When adding new features:
1. Update relevant documentation files in `docs/`
2. Update `README.md` if needed
3. Add examples in appropriate workflow files
4. Update `TASKS.md` if there are new learning objectives

## 🤝 Community Standards

### Be Respectful
- Treat everyone with respect
- Welcome diverse perspectives
- Provide constructive feedback

### Be Helpful
- Answer questions in issues
- Help review PRs
- Share knowledge and resources

### Be Patient
- Learning takes time
- Mistakes happen
- Help others grow

## 📞 Getting Help

- **Questions?** Create an issue using the [question template](.github/ISSUE_TEMPLATE/question.md)
- **Stuck on PR?** Tag maintainers in comments
- **General help?** Reach out to the community

## 🎓 Learning Contribution Ideas

We're always looking for:
- ✅ New workflow examples
- ✅ Additional documentation topics
- ✅ Real-world use cases
- ✅ Best practices guides
- ✅ Tutorial videos or links
- ✅ Practice exercises
- ✅ Integration examples

## 🚀 Your First Contribution

1. Look for issues labeled `good first issue`
2. Comment that you'd like to work on it
3. Ask questions in the issue
4. Submit your PR when ready

## 📊 Recognition

Contributors will be:
- Listed in the project
- Credited in relevant PRs/issues
- Acknowledged for significant contributions

## 📋 Review Process

1. **Automated Checks:** CI/CD pipeline runs
2. **Code Review:** Maintainers review your changes
3. **Feedback:** You might need to make updates
4. **Approval:** When ready, PR is approved
5. **Merge:** Your contribution is merged!

## 💡 Tips for Successful PRs

✅ Keep PRs focused and small  
✅ Write clear commit messages  
✅ Test thoroughly before submitting  
✅ Respond to feedback promptly  
✅ Be patient with the review process  
✅ Ask questions if unsure  

## 🙏 Thank You

Every contribution makes this resource better for future learners. Whether it's a bug fix, documentation update, or new feature, your help is appreciated!

---

**Happy Contributing! 🎉**

For questions about contributing, please open an issue or reach out to the maintainers.
