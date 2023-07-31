# Create-a-Visual-Studio-.NET-Core-Lambda-Project
Built-in Lambda Visual Studio blueprints enable quick project initialization. A blueprint is a canned set of files and functions to quickly demonstrate functionality, and provides a good starting-point for later modifications.

To create a Lambda project
Open Visual Studio, and on the File menu, choose New, Project.

Do one of the following:

For Visual Studio 2017, in the New Project dialog box, expand Installed, expand Visual C#,select AWS Lambda, choose the AWS Lambda Project (.NET Core - C#) template, and then choose OK.



For Visual Studio 2019, in the New Project dialog box, ensure that the Language, Platform, and Project type drop-down boxes are set to "All" and type aws lambda in the Search field. Then choose the AWS Lambda Project (.NET Core - C#) template and choose Next.



Do one of the following:

For Visual Studio 2017, for Name, enter AWSLambda1, enter the desired file Location, and then choose OK.

For Visual Studio 2019, for Name, enter AWSLambda1, enter the desired file Location, and then choose Create.

On the Select Blueprint page, choose the Empty Function blueprint, and then choose Finish to create the Visual Studio project. You can now review the project's structure and code.

Review the Project Files
There are two project files to review: aws-lambda-tools-defaults.json and Function.cs.

The folowing example shows the aws-lambda-tools-defaults.json file, which is created as part of your project. You can set build options by using the fields in this file, which the Lambda tooling reads by default. The project templates in Visual Studio contain many of these fields with default values. The field function-handler specifies the method that runs when the Lambda function runs. If you specify the function-handler field, it is pre-populated in the Publish wizard. If you rename the function, class or assembly then you also need to update the field in the aws-lambda-tools-defaults.json file.


COPY
{
  "Information": [
    "This file provides default values for the deployment wizard inside Visual Studio and the AWS Lambda commands added to the .NET Core CLI.",
    "To learn more about the Lambda commands with the .NET Core CLI execute the following command at the command line in the project root directory.",
    "dotnet lambda help",
    "All the command line options for the Lambda command can be specified in this file."
  ],
  "profile": "default",
  "region": "us-east-2",
  "configuration": "Release",
  "framework": "netcoreapp3.1",
  "function-runtime": "dotnetcore3.1",
  "function-memory-size": 256,
  "function-timeout": 30,
  "function-handler": "AWSLambda1::AWSLambda1.Function::FunctionHandler"
}
Examine the Function.cs file. Function.cs defines the c# functions to expose as Lambda functions. This FunctionHandler is the Lambda functionality that runs when the Lambda function runs. In this project, there is one function defined: FunctionHandler, which calls ToUpper() on the input text.

Your project is now ready to publish to Lambda.

Publish to Lambda
How and when your Lambda functionality is invoked is not a part of the Lambda deployment itself; the Lambda is just the "what" of your on-demand functionality.

To publish your function to Lambda
If the AWS Explorer window is not open, choose View and then choose AWS Explorer.

In Solution Explorer, right-click the project, and then choose Publish to AWS Lambda.

On the Upload Lambda Function page, do the following:


 Upload screen for Lambda function
 

For Package Type, choose Zip. A ZIP file will be created as a result of the build process and will be uploaded to Lambda. The other Package Type option is Image and Tutorial: Basic Lambda Project Creating Docker Image guides you through that alternative.

For Function Name, enter a display name for your Lambda instance. This name is the reference name that both the AWS Explorer within Visual Studio as well as the AWS Management Console display.

(Optional) For Description, enter text to display with your instance in the AWS Management Console.

Choose Next.

In the Advanced Function Details page, do the following:

For Role Name, choose a role associated with your account. The role provides temporary credentials for any AWS service calls made by the code in the function. If you do not have a role, choose New Role based on AWS Managed Policy and then choose AWSLambdaBasicExecutionRole which is a role with minimal access permissions.

Note
Your account must have permission to run the IAM ListPolicies action, or the Role Name list will be empty and you will be unable to continue.

(Optional) If your Lambda function accesses resources on an Amazon VPC, select the subnets and security groups.

(Optional) Set any environment variables that your Lambda function needs. The keys are automatically encrypted by the default service key which is free, or you can specify an AWS KMS key, for which there is a charge. KMS is a managed service you can use to create and control the encryption keys used to encrypt your data. If you have an AWS KMS key, you can select it from the list.

Choose Upload.

The Uploading Function page displays while the function is uploading to AWS. To keep the wizard open after uploading so that you can view the report, clear Automatically close wizard on successful completion at the bottom of the form before the upload completes.

After the function uploads, your Lambda function is live. The Function: view page opens and displays your new Lambda function’s configuration.

To manually invoke the Lambda function, on the Test Function tab enter hello lambda! in the free-text input field and then choose Invoke. Your text, converted to uppercase, will appear in Response.


 Invoking the test function page
 

You can reopen the Function: view at any time by double-clicking on your deployed instance located in the AWS Explorer under the AWS Lambda node.

(Optional) To confirm once more that you successfully published your Lambda function, log into the AWS Management Console and then choose Lambda. The console displays all of your published Lambda functions, including the one you just created.


 Viewing Lamda Functions on AWS Management Console
 

Clean-up
If you are not going to continue developing with this example, delete the function you deployed so that you do not get billed for unused resources in your account.

To delete your function
In the AWS Explorer, under the AWS Lambda node, open the context (right-click) menu for your deployed instance, and then choose Delete.
Next Steps
This example demonstrated how to create a project with a .NET 3.1 managed runtime. For information about how to create a project with a .NET 5.0 custom runtime for your Lambda function, see Exploring .NET 5 with the AWS Toolkit for Visual Studio.

For additional use cases, see Examples of How to Use AWS Lambda.

Lambda automatically monitors Lambda functions for you, reporting metrics through Amazon CloudWatch. To monitor and troubleshoot your function, see Troubleshooting and Monitoring AWS Lambda Functions with Amazon CloudWatch.
