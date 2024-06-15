#### * Make note of region as this will play a big part in this project *
  -- Due to a few issues in AWS, it is highly advisable to use us-west-2/Oregon as your region for this project

### 1. A way to store, update, and pull code
    Create an empty repo in CodeCommit
    
    Add a policy to you IAM user to be able to access CodeCommit
    * Select preferred IAM user and add permissions
    * Attach policies directly
    * Add "AWSCodeCommitPowerUser"
    
    Creat Git credentials for IAM user (This will allow HTTPS connections to CodeCommit)
    * In "Security Credentials" scroll to "HTTPS Git..."
    * Generate Credentials and save values for User/Pass
    
    Clone the repository
    * Select created repo in CodeCommit and Clone HTTPS URL from "Clone URL" dropdown.
      -- This will not actually "clone" the repo but will rather copy the URL that can be used to clone the repo.
    * Open AWS CLI
    * Paste clone URL and enter Username & Password when prompted
      -- These were generated earlier
    * Enter commands:
      ls
      cd <repo-name>
      aws s3 cp s3://ttt-wildrydes/wildrydes-site ./ --recursive
      ls
      git config --gloabl user.email <your-email-address>
      git config --global user.name <your-name>
      git add .
      git commit -m <"commit message">
      git push
      <Enter Username/Password>
      

      
      
    
### 2. A way to handle permissions for code  
    *- Move information from above here -*
    
### 3. A place to host website with permissible updates
    Create a new app for hosting in Amplify
    *  New app -> Host web app -> AWS CodeCommit -> Select repo -> Check Allow AWS...
       -> Select New Service role -> Review, Save and deploy
    ** If deployment fails, refer to text below:
         AWS have also changed the Amplify interface so you don't configure the role as part of the initial 
         setup. However, within the app,  under App settings -> General settings, you can configure the service 
         role after creating the app. I wouldn't have noticed this without your video walkthrough. My service 
         role was automatically set to AdministratorAccess, which had AdministratorAccess permissions, and 
         resulted in failed deployments. This required changing the role to AmplifyConsoleServiceRole (with the 
         AdministratorAccess-Amplify policy) to fix this issue.
         -- Redeploy
    *  Open site URL to confirm site is active

    Open repo in CodeCommit and inspect "index.html" file
    * Edit body section of .html with any text of choice
    * Commit changes
    * Confirm whether changes are visible on the site after redeployment.
        
### 4. A registration and log-in process for users
    Open Cognito service to set up user authentication
    * Create user pool
      -- Choose attributes for sign-in options ->
      -- Choose password policy ->
      -- Choose MFA ->
      -- Enable self registration ->
      -- Choose "send email with Cognito ->
      -- Enter user pool name, enter app client name ->
      -- Review, create
    * Store User pool ID, App Client ID (found in App Integration tab)
      -- Hold values in text editor of choice

    Inspect "config.js" file in CodeCommit
    * Edit file and insert values for UserPoolID, UserPoolClientId, and region
      -- These are the values for User pool ID and App Client ID that were stored in the previous step. For 
         region, use current region.
    * Commit changes
    * Confirm whether changes are visible on the site after redeployment
      -- Open site and register by pressing "Giddy Up!"
      -- Verify email
      -- Sign In (Should recieve a "Successfully Authenticated" message)
    
### 5. A way to do ride sharing functionality
    Implement ride share functionality with DynamoDB
    * Create Table (in Tables option)
      -- Enter Table name
      -- Enter Partition key, add "Id" to whatever name is set, set to string
      -- Create table
    * Inspect newly created table
      -- Under General Information, expand Additional info
      -- Copy and store ARN

    Creat new role in IAM
    * Create new role
      -- AWS Service, Lambda ->
      -- Search and select "AWSLambdabasicExecutionRole" ->
      -- Assign name for role ->
      -- Create role
    * Select newly created role
    * Add permissions
      -- Create inline policy
      -- Choose DynamoDB service
      -- Search and select "PutItem"
      -- In resources, choose "Specific" and add stored ARN from DynamoDB table ->
      -- Enter policy name
      -- Create policy

    Implement ride share functionality with Lambda
    * Create function
      -- Author from scratch, enter function name
      -- Use Node.js 16x for Runtime
      -- Select an existing role (select newly created role made for DynamoDB)
      -- Create function
    * Inspect index.js code
    * Replace sample code with code from Lambda function code
      ++ Refer to "RequestUnicorn_LambdaFunction" file provided in repo
      ++ Only use code from Lambda Function section
      ++ Values for certain parameters MUST be replaced to match names and strings of your entered values.
    * Configure test event (Under Test button dropdown)
      -- Assign an event name
      -- Replace sample code with Test Event code
        ++ Refer to "RequestUnicorn_LambdaFunction" file provided in repo
        ++ Only use code from Test Event section
      -- Save
      -- Test, verify that statusCode: 201 is received (This means test ran successfully)
        ++ If statusCode is not 201, review code and configure variables
       
### 6. A place to store and return ride results
    Check Dynamo DB table to confirm if values were written as a result of test event
    * Select table from DynamoDB service
      -- Explore table items
        ++ This button may have been removed due to UI updates.
      -- Verify if unicorn value was generated.
      -- Inspect unicorn
      
### 7. A way to invoke ride sharing functionality
    

