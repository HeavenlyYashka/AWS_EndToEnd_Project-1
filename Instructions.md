#### * Make note of region as this will play a big part in this project *
  -- Due to a few issues in AWS, it is highly advisable to use us-west-2/Oregon

### 1. A way to store, update, and pull code
    <b> Create an empty repo in CodeCommit </b>
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
    
    
2. A way to handle permissions for code
3. A place to host website with permissible updates
4. A registration and log-in process for users
5. A way to do ride sharing functionality
6. A place to store and return ride results
7. A way to invoke ride sharing functionality

