# 🚀 CI Template: Deploy to S3 + CloudFront

This CI pipeline streamlines the **building and deployment of static applications** to an **S3 bucket**, coupled with **automatic CloudFront cache invalidation**.

-----

## ✅ Features

  * **App Build Process**: Automates the build of your static application.
  * **S3 Upload with Cache-Control**: Efficiently uploads your built application to S3 with optimized cache control settings.
  * **Automatic CloudFront Invalidation**: Ensures immediate content updates by invalidating CloudFront cache after deployment.
  * **Multi-environment Support**: Configurable for different deployment environments (e.g., Stage, Production).

-----

## ⚙️ How to Use

### Project Configuration

To ensure dynamic routing and seamless integration, configure your frontend project (e.g., with Vite + React) as follows:

  * **React Router DOM**: When using `react-router-dom` with `createBrowserRouter`, set the `basename` using the environment variable `REACT_APP_BROWSER_ROUTER_BASENAME`. This variable will be exposed during the CI build process.
  * **Vite Configuration**: In your `vite.config.ts`, define the `base` property like this:
    ```typescript
    base: process.env.REACT_APP_BROWSER_ROUTER_BASENAME || '/',
    ```

### GitHub Actions Workflow Files

To set up the CI/CD pipeline, you need to create a `.github/workflows` folder in the root of your repository. Inside this folder, add the following workflow files:

  * `start_clear_preview.yml`
  * `start_push_preview.yml`
  * `start_push_prod_release.yml`
  * `start_push_stage_release.yml`

### GitHub Actions Secrets

For the CI pipeline to function correctly, you must add the following **secrets** to your repository's "Actions" settings:

#### Stage Secrets

These secrets are prefixed with `STAGE_` for your staging environment:

  * `STAGE_AWS_ACCESS_KEY_ID`: Your AWS IAM access key ID.
  * `STAGE_AWS_SECRET_ACCESS_KEY`: Your AWS IAM secret access key.
  * `STAGE_AWS_REGION`: The AWS region where your S3 bucket is located.
  * `STAGE_S3_BUCKET_NAME`: The name of your S3 bucket for the stage environment.
  * `STAGE_CLOUDFRONT_DISTRIBUTION_ID`: The CloudFront distribution ID for the stage environment.
  * `STAGE_WF_GITHUB_TOKEN`: A GitHub classic token with `repo` permissions, used for workflow operations.
  * `STAGE_DOMAIN`: The base S3 domain for app review link exposure.
  * `STAGE_GH_LINK_PROJECT_ENVS`: Private GitHub repository link of environment variables specific to your stage project. 

    ⚠️ **This must be the raw URL** of the `.env` file in a private GitHub repository, allowing direct download of environment variables content, not a web interface link.

  * `STAGE_GH_LINK_PR_PROJECT_ENVS`: Private GitHub repository link of custom open pull-request environment variables specific to your stage. `OPTIONAL`

    ⚠️ **This must be the raw URL** of the `.env` file for the pull request environment in a private GitHub repository, enabling direct access to the raw environment variables.

#### Production Secrets

These secrets are for your production environment:

  * `AWS_ACCESS_KEY_ID`: Your AWS IAM access key ID.
  * `AWS_SECRET_ACCESS_KEY`: Your AWS IAM secret access key.
  * `AWS_REGION`: The AWS region where your S3 bucket is located.
  * `S3_BUCKET_NAME`: The name of your S3 bucket for the production environment.
  * `CLOUDFRONT_DISTRIBUTION_ID`: The CloudFront distribution ID for the production environment.
  * `WF_GITHUB_TOKEN`: A GitHub classic token with `repo` permissions, used for workflow operations.
  * `GH_LINK_PROJECT_ENVS`: Private GitHub repository link of environment variables specific to your default project environment (e.g., production or development).  
  ⚠️ **This must be the raw URL** of the `.env` file stored in a private GitHub repository to ensure the pipeline can fetch the raw environment variables content directly.

### PUSH PREVIEW CI INPUTS

- `run_tests`: Enables or disables running the test suite and uploading the coverage report.  
- `run_lint`: Enables or disables the commit message linting step.  
- `run_tsc`: Enables or disables the TypeScript build and type checking step.