# Build-Full-End-to-End-Web-APP

## Objective

This project aimed to teach how to build and deploy AWS services resulting in a ride sharing application. 

### Skills Learned

- How to store/update/pull code (Git add, Git push, Git clone)
- Handle persmissions for code
- A place to host website and make updates
- A way for users to register and login
- A way to do ride sharing functionality
- Somewhere to store/return ride results
- A way to invoke ride sharing functionality

### Tools Used

- CodeCommit
- Amplify
- Cognito
- Lambda
- IAM
- API Gateway
- DynamoDB

## Steps

*Ref 1: Network Diagram*![what i build](https://github.com/ShawntaG/Deploy-Full-End-to-End-Web-APP/assets/132296632/0fe439bb-92bc-4800-b07e-243ea6f62a0d)

*Code Files provided by AWS*

Create Empty Repository in CodeCommit

![image](https://github.com/ShawntaG/Deploy-Full-End-to-End-Web-APP/assets/132296632/6730dd27-b571-4d00-90d5-e92b185d6b77)

Add a policy to your IAM user so you can access CodeCommit

Creat Git credentials for you IAM user to allow HTTPS connections to CodeCommit. Copy or download your Username and Password that was generated.

![image](https://github.com/ShawntaG/Deploy-Full-End-to-End-Web-APP/assets/132296632/78e3b8a0-44c8-45ed-81e6-6733fb81565c)

Clone the repository (copy the URL).

![image](https://github.com/ShawntaG/Deploy-Full-End-to-End-Web-APP/assets/132296632/a8f791f6-da4d-4ec4-b251-cb9da11714ab)

Open Cloud Shell

Run  "Git clone" and paste url. 

![image](https://github.com/ShawntaG/Deploy-Full-End-to-End-Web-APP/assets/132296632/61b420e7-0f80-422d-99f2-4cef8b90b54d)

Enter username in the next line that was generated from your IAM user HTTPS Git credentials.

Enter password generated from the same credentials.

You can run "ls" command to see the folder in the directory.

![image](https://github.com/ShawntaG/Deploy-Full-End-to-End-Web-APP/assets/132296632/171fa32a-9783-444a-804a-b27963c4e1f0)

Copy the project code from the S3 bucket and commit it to the new repo by changing the directory to that folder and import the code from the s3 bucket provided. Command provided in the screenshot. 

![image](https://github.com/ShawntaG/Deploy-Full-End-to-End-Web-APP/assets/132296632/1eb4abf4-617a-4490-b642-564183bc68e4)

Run the following commands to add the files to the folder, add commment, verify credentials and push the code. 
1. git add .
2. git commit -m "Initial Commit"
3. [Enter Credentials] Same UN and PW from IAM user credentials generated for HTTPS git access. 
4. git commit -m "Initial Commit"
5. git push

Use AMPLIFY to host web app. 

1.Navigate to amplify
2.Click new app
3.Host web app
4.Choose CodeCommit
5.Selecty Repository

Test Web App

Use Cognito to authenticate users.

1.Create new user pool
2.User name
3.Choose MFA settings
4.Set email settings

Update config file in the application code to point to the new user pool. 

For this you will need the User Pool ID and the Client ID

Commit Changes

Test Web App

![image](https://github.com/ShawntaG/Deploy-Full-End-to-End-Web-APP/assets/132296632/ebd6deb8-37ea-4194-ad73-467392f96c6a)

Map is not yet setup. Copy the token to a notepad for later use. 

![image](https://github.com/ShawntaG/Deploy-Full-End-to-End-Web-APP/assets/132296632/9c671d31-f0c9-4ecc-bdf5-4e66527c0bf8)\

Create a Lambda function and a NoSQL database using DynamoDB

After creating DynamoDB table, copy the ARN for later user. 

Next we need to create an IAM role to be able to execute Lambda functions

Add new permissions to user role.

1. Choose Lambda service

   ![image](https://github.com/ShawntaG/Deploy-Full-End-to-End-Web-APP/assets/132296632/69ccc9aa-0632-440a-bc25-158097aef13d)

2. Choose "AWS Lambda Basic Execution Role" policy
   
![image](https://github.com/ShawntaG/Deploy-Full-End-to-End-Web-APP/assets/132296632/e1d7b1f6-6567-4cd1-a045-17fcf4b0d00e)


3. Choose name for role
4. Open created role
5. Add new permission
   
   ![image](https://github.com/ShawntaG/Deploy-Full-End-to-End-Web-APP/assets/132296632/fc1fe33d-a292-44d3-8c08-981d15570d24)

6. Create inline policy (will allow you to write to a DynamoDB table).
7. Choose DynamoDB as the service
    
    ![image](https://github.com/ShawntaG/Deploy-Full-End-to-End-Web-APP/assets/132296632/f9326d35-abbf-46ab-a3b1-8be11ec83d25)

8. Choose "putitem" as the action allowed
9. Add the "ARN" copied earlier and pase it in the resources. (This specifies what table you are able to write to.)

![image](https://github.com/ShawntaG/Deploy-Full-End-to-End-Web-APP/assets/132296632/ae144b00-42a9-425e-8e31-c129a1f57c96)

Create new Lambda function

Choose "Node.js 16.x as the language. 

Use existing rolde and choose the role created earlier

Create function.

Add code provided by AWS. 

Deploy Code

Now we need to test the code. 

Click Test Code. 

![image](https://github.com/ShawntaG/Deploy-Full-End-to-End-Web-APP/assets/132296632/529f192a-b543-4530-9f0b-249a26044252)

Add test code and run the test. 

There should be an entry in your DynamoDB table if successful

![image](https://github.com/ShawntaG/Deploy-Full-End-to-End-Web-APP/assets/132296632/4748d6ef-52b9-4498-9076-5fa08c511cc7)

Next we need something to invoke the ride sharing functionality. We will use the API Gateway service. 

Create new API

Choose RestAPI

Create a name

Choose Edge-optimized as the endpoint type.

Next we need to create an authorizer

![image](https://github.com/ShawntaG/Deploy-Full-End-to-End-Web-APP/assets/132296632/5aa1394f-2191-46cd-916d-1404d2192c7f)

User Cognito as the type

Choose your user pool

Enter Authorizer as the token source

![image](https://github.com/ShawntaG/Deploy-Full-End-to-End-Web-APP/assets/132296632/0df32343-a150-4158-a9ec-4d3012836009)

Test authorizer and enter token copied earlier. 

![image](https://github.com/ShawntaG/Deploy-Full-End-to-End-Web-APP/assets/132296632/eed8784b-dae6-4f27-bd7f-904f25b7be2e)

Create a resource in your API

Make sure to enable CORS

Next create methode while the resource you created is selected. 

![image](https://github.com/ShawntaG/Deploy-Full-End-to-End-Web-APP/assets/132296632/b1b3baf6-cbe7-447f-b32d-1d86762cc15b)

Choose "POST" as the method type

Enable 'Lambda proxy integration"

Choose your Lambda function

Create method.

Edit method request

![image](https://github.com/ShawntaG/Deploy-Full-End-to-End-Web-APP/assets/132296632/af32f732-67ca-4524-9631-ae8cce0209b9)

Choose your user pool as the authorization.

Deploy API

Copy Invoke URL

Add Invoke URL to the code in CodeCommit

![image](https://github.com/ShawntaG/Deploy-Full-End-to-End-Web-APP/assets/132296632/6aaea77f-b722-46ac-8b8a-e12c1e13a207)

Commit changes. 

Test Web Application

![image](https://github.com/ShawntaG/Deploy-Full-End-to-End-Web-APP/assets/132296632/93be134f-256e-4c15-8cde-534ad2e3f741)

Shut down resources. 
















































   

















