# Sample to deploy React SSR on Lambda

This repository consists of a sample to demonstrate two variants to do Server Side Rendering with AWS Lambda for React applications.
It usues AWS CDK to make the deployment.


## Folder structure

- /cdk - code to deploy the solution 
- /simple-ssr - React application created with the create-react-app tool.

## DEMO
```
SSRAppStack.Bucket = ssr-site
SSRAppStack.CFURL = https://d2xahn4a9ak7lb.cloudfront.net
SSRAppStack.LambdaEdgeSSRURL = https://d2xahn4a9ak7lb.cloudfront.net/edgessr
SSRAppStack.LambdaSSRURL = https://d2xahn4a9ak7lb.cloudfront.net/ssr
SSRAppStack.SSRAPIURL = https://atfahc5h54.execute-api.us-east-1.amazonaws.com/prod/
SSRAppStack.ssrEndpoint02F5615F = https://atfahc5h54.execute-api.us-east-1.amazonaws.com/prod/

```

## Deployment

- Run the following commands in your terminal window, provide the name of the S3 bucket instead of `ssr-react`, for example `mybucket`, to deploy the static content

    `cd react-ssr-lambda`

    `cd ./cdk`

    `yarn`

    `yarn build`

    `cdk bootstrap`

    `cdk deploy SSRApiStack --outputs-file ../simple-ssr/src/config.json`

    `cd ../simple-ssr`

    `yarn`

    `yarn build-all`

    `cd ../cdk`

    `cdk deploy SSRAppStack --parameters mySiteBucketName=ssr-react`

- After successful deployment you will see output variables

    **CF URL** - for React App stored on S3 and rendered on client

    **Lambda SSR URL** - for React App rendered by Lambda behind API Gateway

    **Lambda@Edge SSR URL** - for React App rendered by Lambda@Edge

## Clean UP

- To clean-up the reated resources run

    `cd ./cdk`

    `cdk destroy SSRApiStack`
    
    `cdk destroy SSRAppStack`