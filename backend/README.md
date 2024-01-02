## AWS AppSync Backend Setup
 ### Services
- AWS AppSync
- AWS Lambda
- Amazon DynamoDB
- Serverless Framework for IaC
- GitHub actions configured to run jobs for dev/prod deployment
- Webpack for bundling code
- ESLint for formatting, linting etc.

### Steps to setup and deploy

#### `npm install`
- This will install all the required dependencies.

#### `npm run format`
- format all the files using ESLint

#### `npm run bundle`
- Packages the code using WebPack

#### `serverless deploy`
- This command will deploy the resources to AWS using dev credentials


### GitHub Actions Workflow
#### Steps to setup jobs using GitHub Actions
The following is the list of steps that is executed as a part of the job setup:

1. Store all account credentials in GitHub secrets to access them in environment without exposing. The AWS credentials will be used for deploying the application into your AWS account.
```
AWS_ACCESS_KEY_ID: ${{secrets.AWS_ACCESS_KEY_ID}}
AWS_SECRET_ACCESS_KEY: ${{secrets.AWS_SECRET_ACCESS_KEY}}
DEV_REGION: ${{secrets.DEV_REGION}}
PROD_REGION: ${{secrets.PROD_REGION}}
```
An alternative approach is to run this command directly from cmd with github actions. 
```
serverless config credentials --provider aws --key <Access Key ID> --secret <Secret Access Key> --region <Region>
```
 
2. Install serverless
3. Install npm
6. Build project using webpack
7. Deploy to dev environment: Mumbai (ap-south-1)
8. Deploy to prod environment: Oregon (us-west-2)
