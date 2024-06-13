#### * Make note of region as this will play a big part in this project *
  -- Due to a few issues in AWS, it is highly advisable to use us-west-2/Oregon

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
    * In Amplify service:
      -- New app -> Host web app -> AWS CodeCommit -> Select repo -> Check Allow AWS...
         -> Select New Service role -> Review, Save and deploy
    ** If deployment fails, refer to text below:
        AWS have also changed the Amplify interface so you don't configure the role as part of the initial setup.
        However, within the app,  under App settings -> General settings, you can configure the service role 
        after creating the app. I wouldn't have noticed this without your video walkthrough. My service role was 
        automatically set to AdministratorAccess, which had AdministratorAccess permissions, and resulted in 
        failed deployments. This required changing the role to AmplifyConsoleServiceRole (with the 
        AdministratorAccess-Amplify policy) to fix this issue.
        
4. A registration and log-in process for users
5. A way to do ride sharing functionality
6. A place to store and return ride results
7. A way to invoke ride sharing functionality

