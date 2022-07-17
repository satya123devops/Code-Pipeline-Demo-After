# PROJECT_NAME


## Getting Started

If you haven't already you should create a GitHub repository for this project via [ServiceNow](https://lilly.service-now.com), search for "GitHub Services". You can clone the repository that ServiceNow creates
and copy your project files into that new directory. Once you have copied your files over it is heavily recommended to create an initial commit with the files exactly as they were
created. This provides a point in the git history where you can find what what originally created for you.

In order to deploy your SPA you will need to create an AWS deployment pipeline.
To create the pipeline, create a new CloudFormation stack using [the v2 deployment pipeline template](https://lly-templates.s3.us-east-2.amazonaws.com/shared/cloudformation/deployment_pipelines_v2/cfn-pipeline.yaml).
Once your pipeline has been created you will be able to deploy your template just by pushing code to GitHub.

## Web Application Expectations
The build process in CodeBuild attempts to run `npm install`, `npm test`, `npm lint`, and `npm build`. If there are any operations that need to occur to prepare your web application for deployment they need to be
triggered by the `build` script in your `package.json` file. CodeBuild will upload the files from the `./build/` directory.

## Lambda@Edge Authorization
This application can be configured to use Lambda@Edge authorization. This is done by setting the `CloudFrontRequireAuth` template parameter to `true`.
If you enable Lambda@Edge authorization, you will only be able to deploy your application to the `us-east-1` region. This is a limitation of Lambda@Edge.

## Directory Structure

```
.
├── buildspec.yml                     <-- CodeBuild file able to install and bundle your SPA
├── package-lock.json                 <-- Node dependencies file
├── package.json                      <-- Node dependencies file
├── params.dev.json                   <-- CloudFormation dev environment configuration
├── params.prod.json                  <-- CloudFormation prod environment configuration
├── params.qa.json                    <-- CloudFormation qa environment configuration
├── post-deploy-buildspec.yml         <-- CodeBuild file to check your code and upload it
├── public/                           <-- Directory containing resources that will be uploaded with your application
├── README.md                         <-- This instructions file
├── src/                              <-- Directory containing web application code
└── template.yml                      <-- Application deployment resources CloudFormation template
```