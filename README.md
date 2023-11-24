# AWS CI/CD Pipeline with Elastic Beanstalk and CodePipeline

This repository demonstrates a Continuous Integration and Continuous Deployment (CI/CD) pipeline using AWS services such as Elastic Beanstalk, CodePipeline, and GitHub Actions. The pipeline is set up to automatically deploy a Python web application whenever changes are pushed to the specified branch in the GitHub repository.

## Prerequisites

Before getting started, make sure you have the following:

- An AWS account.
- IAM Role: `master1` with the `AmazonSSMFullAccess` policy attached.

## Elastic Beanstalk Environment Setup

1. Create an Elastic Beanstalk environment to deploy your Python web application.

2. Configure the environment settings, including the application name, environment name, and platform version.

3. Select the Python platform for your application.

4. Configure service access and attach the `master1` IAM role to the EC2 instance profile.

5. Customize other settings like instance type, security, and environment variables if needed.

6. Click "Submit" to create the environment.

## Sample Application

The sample Python application provided in this repository is based on the Elastic Beanstalk default Python application. The main modification is in the `application.py` file and the addition of the `.ebextensions` folder containing the `python.config` file.

## CodePipeline Setup

1. Create a CodePipeline to automate the deployment process.

2. Configure the source stage to connect to your GitHub repository, selecting the branch to trigger the pipeline.

3. Optionally, configure a build stage using CodeBuild or another build tool if needed.

4. In the deploy stage, choose Elastic Beanstalk as the deployment provider and select the application and environment created in the Elastic Beanstalk setup.

5. Click "Create pipeline" to finalize the pipeline configuration.

## Output

Any changes committed to the specified branch in your GitHub repository will trigger the pipeline, automatically deploying the updated application to the Elastic Beanstalk environment.

## Additional Notes

Ensure that your project repository includes the necessary deployment scripts and configurations, such as the `python.config` file, to enable a smooth deployment process.

Feel free to explore and customize the pipeline according to your project's specific requirements.

## Python.config File Explanation

The `python.config` file in the `.ebextensions` folder contains configuration settings for the Elastic Beanstalk environment:

```yaml
option_settings:
  "aws:elasticbeanstalk:container:python":
    WSGIPath: application:application
```

- **option_settings:** This section allows you to specify various settings for different components of your environment.

- **"aws:elasticbeanstalk:container:python":** Identifies the specific configuration option for the Python container within Elastic Beanstalk.

- **WSGIPath:** Specifies the entry point to your Python application. It consists of two parts separated by a colon. The first part refers to the Python module (Python file), and the second part specifies the callable object (e.g., a function or an instance of a WSGI application) within the Python module that serves as the entry point for your web application. In this case, it's set to `application:application`.
