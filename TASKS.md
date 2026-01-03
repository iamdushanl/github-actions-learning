# 🎓 GitHub Actions Learning Tasks

This file contains hands-on exercises to help you master GitHub Actions. Complete these tasks to solidify your understanding!

## Beginner Tasks ⭐

### Task 1: Run Your First Workflow
**Objective:** Understand how workflows execute

**Steps:**
1. Go to your repository
2. Click the "Actions" tab
3. Find the "Hello World Workflow"
4. Click "Run workflow" → "Run workflow" button
5. Watch it execute in real-time
6. Check the logs to see all the outputs

**What You'll Learn:**
- How to trigger workflows manually
- How to read workflow logs
- Understanding GitHub context variables

**Completion:** ✅ Expand the workflow job and verify you can see all the echo outputs

---

### Task 2: Understand Workflow Triggers
**Objective:** Learn when workflows are triggered

**Steps:**
1. Edit `.github/workflows/hello-world.yml`
2. Make a small change (add a comment)
3. Commit and push to `main`
4. Go to Actions tab and verify the workflow ran automatically
5. Check the workflow was triggered by `push` event

**What You'll Learn:**
- How push events trigger workflows
- The difference between manual and automatic triggers

**Completion:** ✅ The workflow should run automatically when you push

---

### Task 3: Build and Test Locally
**Objective:** Run the sample app and tests locally

**Steps:**
```bash
cd sample-app
npm install
npm test
npm start
```

5. Visit `http://localhost:3000` in your browser
6. Test different API endpoints

**What You'll Learn:**
- How the sample application works
- Running tests locally
- Testing API endpoints

**Completion:** ✅ All tests pass and the server starts without errors

---

## Intermediate Tasks ⭐⭐

### Task 4: Create a Custom Workflow
**Objective:** Build your own GitHub Actions workflow

**Steps:**
1. Create `.github/workflows/custom.yml`
2. Add a workflow that:
   - Triggers on push to `develop` branch
   - Sets up Node.js 18
   - Runs: `npm install && npm test` in the `sample-app` directory
3. Commit and push to the `develop` branch
4. Verify the workflow runs in Actions tab

**Example to get started:**
```yaml
name: Custom Workflow
on:
  push:
    branches: [develop]

jobs:
  custom-job:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      # Add more steps...
```

**What You'll Learn:**
- Creating workflows from scratch
- Working with different branches
- Configuring workflows for specific directories

**Completion:** ✅ Your custom workflow runs successfully on the develop branch

---

### Task 5: Add Environment Variables
**Objective:** Use environment variables in workflows

**Steps:**
1. Edit `.github/workflows/build-test.yml`
2. Add environment variables at the job level:
   ```yaml
   env:
     NODE_ENV: test
     LOG_LEVEL: debug
   ```
3. Add a step to print these variables:
   ```yaml
   - name: Print environment
     run: |
       echo "Environment: ${{ env.NODE_ENV }}"
       echo "Log Level: ${{ env.LOG_LEVEL }}"
   ```
4. Push the changes and verify the workflow logs show the values

**What You'll Learn:**
- Setting environment variables in workflows
- Accessing environment variables in steps
- Job-level vs global environment variables

**Completion:** ✅ Environment variables are printed in the workflow logs

---

### Task 6: Use GitHub Secrets
**Objective:** Practice working with secrets (without exposing real credentials)

**Steps:**
1. Create a test secret:
   - Settings → Secrets and variables → Actions
   - New secret: `TEST_SECRET` = `my-secret-value`
2. Edit `.github/workflows/hello-world.yml`
3. Add a step:
   ```yaml
   - name: Access secret
     run: echo "Secret length: ${#{{ secrets.TEST_SECRET }}}"
   ```
4. Push and verify in logs (secret won't be displayed)

**What You'll Learn:**
- Creating and storing secrets
- Using secrets in workflows
- How GitHub masks secrets in logs

**Completion:** ✅ Workflow runs successfully and secret is masked in logs

---

### Task 7: Matrix Testing
**Objective:** Test across multiple configurations

**Steps:**
1. Look at `.github/workflows/build-test.yml` which already has matrix configuration
2. Understand how it tests multiple Node versions
3. Modify the matrix to test 3 different Node versions:
   ```yaml
   strategy:
     matrix:
       node-version: [16.x, 18.x, 20.x]
   ```
4. Push and verify it creates 3 parallel job runs

**What You'll Learn:**
- Using matrix strategy for multiple configurations
- Parallel job execution
- Testing compatibility across versions

**Completion:** ✅ Workflow runs 3 jobs in parallel for different Node versions

---

## Advanced Tasks ⭐⭐⭐

### Task 8: Upload and Download Artifacts
**Objective:** Pass data between jobs using artifacts

**Steps:**
1. Edit `.github/workflows/build-test.yml`
2. After the build step, add:
   ```yaml
   - name: Create artifact
     run: echo "Build output" > output.txt
   
   - name: Upload artifact
     uses: actions/upload-artifact@v3
     with:
       name: build-output
       path: output.txt
   ```
3. Add a new job that depends on this job and downloads the artifact
4. Push and verify artifacts in the Actions UI

**What You'll Learn:**
- Uploading artifacts
- Downloading artifacts
- Job dependencies
- Artifact persistence

**Completion:** ✅ Artifact is uploaded and can be downloaded from Actions UI

---

### Task 9: Conditional Execution
**Objective:** Run steps conditionally based on events/conditions

**Steps:**
1. Create `.github/workflows/conditional.yml`
2. Add workflow with steps that only run on `main` branch:
   ```yaml
   - name: Deploy (main only)
     if: github.ref == 'refs/heads/main'
     run: echo "Deploying to production..."
   ```
3. Test by pushing to `develop` - deployment step should be skipped
4. Push to `main` - deployment step should run

**What You'll Learn:**
- Using `if` conditions in workflows
- GitHub context variables
- Conditional job/step execution

**Completion:** ✅ Steps execute/skip based on branch conditions

---

### Task 10: Create a PR and Use Issue Templates
**Objective:** Practice contribution workflow with templates

**Steps:**
1. Fork this repository (if it's on GitHub)
2. Create a new branch: `git checkout -b feature/my-feature`
3. Make a small change to the sample app
4. Commit and push: `git push origin feature/my-feature`
5. Create a Pull Request from your fork
6. Use the PR template to describe your changes
7. In Issues tab, create an issue using one of the templates

**What You'll Learn:**
- GitHub workflow (fork, branch, PR)
- Using contribution templates
- Community participation

**Completion:** ✅ PR and Issue created with proper template format

---

## Challenge Tasks 🏆

### Challenge 1: Deploy to Azure (Optional)
**Objective:** Deploy the sample app to Azure App Service

**Requirements:**
- Azure account (free tier available)
- Create an App Service
- Set up Azure credentials as GitHub secret
- Deploy using `.github/workflows/deploy-azure-app-service.yml`

**Steps:**
1. Create Azure App Service
2. Create service principal for authentication
3. Add `AZURE_CREDENTIALS` secret
4. Push to main branch
5. Monitor deployment in Actions tab
6. Verify app is running on Azure

**What You'll Learn:**
- Azure App Service deployment
- GitHub Secrets for production credentials
- Multi-stage deployments (staging → production)

**Completion:** ✅ App is deployed and accessible at Azure URL

---

### Challenge 2: Add Code Coverage Reports
**Objective:** Generate and track code coverage

**Steps:**
1. Modify `.github/workflows/build-test.yml`
2. Add coverage reporting:
   ```yaml
   - name: Upload coverage
     uses: codecov/codecov-action@v3
     with:
       files: ./sample-app/coverage/coverage-final.json
   ```
3. Push and verify coverage report is uploaded
4. Check Codecov dashboard

**What You'll Learn:**
- Code coverage reporting
- Integration with external services
- Quality metrics tracking

**Completion:** ✅ Coverage reports are generated and uploaded

---

### Challenge 3: Create a Custom Action
**Objective:** Build your own reusable GitHub Action

**Steps:**
1. Create `.github/actions/hello-world-action/action.yml`
2. Define inputs and outputs
3. Add JavaScript or composite action steps
4. Use it in a workflow
5. Document how to use it

**What You'll Learn:**
- Custom action creation
- Action structure and configuration
- Reusable workflow components
- Sharing actions with community

**Completion:** ✅ Custom action works and can be used in workflows

---

## Completion Checklist

Track your progress:

- [ ] **Beginner (1-3):** Hello World, Triggers, Local Testing
- [ ] **Intermediate (4-7):** Custom Workflow, Env Vars, Secrets, Matrix
- [ ] **Advanced (8-10):** Artifacts, Conditionals, PR/Issues
- [ ] **Challenge:** Azure Deployment, Coverage, Custom Action

## Additional Learning

After completing these tasks:

1. **Read the Documentation:** Review all files in the `docs/` folder
2. **Explore Workflows:** Understand how each example workflow works
3. **Modify Workflows:** Change triggers, steps, and conditions
4. **Experiment:** Create your own workflows for your projects
5. **Share:** Help others and contribute improvements

## Resources

- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [GitHub Actions Marketplace](https://github.com/marketplace?type=actions)
- [Sample App README](sample-app/README.md)
- [Azure Documentation](https://docs.microsoft.com/en-us/azure/)

## Getting Help

If you're stuck:

1. Check the [documentation](docs/)
2. Review the example workflows in `.github/workflows/`
3. Create an issue using the [question template](.github/ISSUE_TEMPLATE/question.md)
4. Check GitHub Actions logs for error messages

---

**🎉 Congratulations on starting your GitHub Actions learning journey!**

Each task you complete makes you more proficient with automation and CI/CD. Keep practicing and you'll become a GitHub Actions expert!

**Happy Learning! 🚀**
