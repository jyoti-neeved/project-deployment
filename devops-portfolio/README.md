# DevOps Portfolio — GitHub Actions + AWS Amplify manual deployment

This is a static HTML/CSS/JavaScript website. GitHub Actions packages the website and deploys it to an AWS Amplify app that was created using **Deploy without Git**.

## Files
- `index.html` — website content
- `styles.css` — responsive design
- `script.js` — mobile navigation and current year
- `.github/workflows/deploy.yml` — GitHub Actions deployment workflow

## Before the first push
1. Create an Amplify app in the AWS Console using **Deploy without Git** and the manual deployment method.
2. Create/select a branch named `main` in that manual app.
3. Configure a GitHub OIDC provider in IAM.
4. Create an IAM role with a trust policy restricted to `repo:YOUR_USERNAME/YOUR_REPOSITORY:ref:refs/heads/main`.
5. Grant the role `amplify:CreateDeployment` and `amplify:StartDeployment` permissions for the target app/branch where supported by the IAM authorization reference.
6. In GitHub repository Settings → Secrets and variables → Actions → Variables, add:
   - `AWS_ROLE_ARN`
   - `AWS_REGION`
   - `AMPLIFY_APP_ID`
   - `AMPLIFY_BRANCH` (set to `main`)

## Run locally
Open `index.html` in your browser, or use VS Code Live Server.

## Deploy
Push the code to the `main` branch. GitHub Actions validates and zips the static site, uploads it using Amplify's temporary deployment URL, then starts the deployment.

## Notes
- This workflow is for static websites, not Next.js SSR.
- The sample portfolio uses placeholder contact details and should be personalized before publishing.
- Pin GitHub Actions to verified commit SHAs for a stricter production supply-chain policy.
