# deploy.yml Workflow Analysis

# 1. What triggers this workflow to run?
The workflow is triggered by:

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

- Push to the main branch
- Pull request targeting the main branch

Any push or PR to another branch will not trigger this workflow.

# 2. What are the four main steps this workflow performs?
Job: build-and-test
1. Checkout code – "Checkout code"
2. Validate HTML – "Validate HTML"
3. Check links – "Check links"
4. Upload artifact – "Upload artifact"

Job: deploy
- Deploy to GitHub Pages – "Deploy to GitHub Pages"

The four main actions in order are:
1. Checkout code
2. Validate HTML
3. Check links
4. Upload artifact for deployment

# 3. What does the "Checkout code" step do and why is it necessary?
- Pulls the repository’s code into the workflow runner
- Necessary because without the code, the workflow cannot validate HTML, check links, or deploy the site

# 4. What is the purpose of the environment configuration?
environment:
  name: github-pages
  url: ${{ steps.deployment.outputs.page_url }}

- Specifies the deployment environment (github-pages)
- Provides a URL output for the deployed site
- Helps GitHub track deployments, review changes, and manage environment-specific permissions

# 5. How does this automated deployment improve reliability compared to manual deployment?
- Ensures consistent execution of deployment steps
- Reduces human error (e.g., forgetting files, misconfiguring settings)
- Automatically validates HTML and checks links before deployment
- Deploys only if tests pass, ensuring the live site works correctly
- Provides a clear audit trail of all deployments

# 6. What would happen if you pushed code to a different branch (not main)?
- The workflow would not run because it is configured to trigger only on push or pull_request events targeting main
- No deployment, HTML validation, or link checking would occur for other branches
