Configure your AWS credentials using the AWS CLI or by creating a ~/.aws/credentials file.

To configure your AWS credentials, you can use the AWS CLI or manually create the ~/.aws/credentials file. Here’s how to do both:
Using AWS CLI

    Install AWS CLI: If you haven't installed the AWS CLI, follow the installation guide for your operating system.
    Configure Credentials: Open your terminal and run the following command:
    aws configure
You will be prompted to enter your AWS Access Key ID, Secret Access Key, default region name, and output format:
AWS Access Key ID [None]: YOUR_ACCESS_KEY_ID
AWS Secret Access Key [None]: YOUR_SECRET_ACCESS_KEY
Default region name [None]: us-west-2  # Replace with your preferred region
Default output format [None]: json  # You can choose json, yaml, text, or table
This command creates the necessary configuration files automatically.
Manually Creating ~/.aws/credentials File

If you prefer to do it manually:

    1. Create the Directory: If it doesn’t already exist, create the .aws directory in your home folder:
    mkdir -p ~/.aws
    2. Create the Credentials File: Open (or create) the credentials file:
    nano ~/.aws/credentials
    3. Add Your Credentials: Add the following lines, replacing the placeholders with your actual AWS Access Key and Secret Access Key:
    [default]
    aws_access_key_id = YOUR_ACCESS_KEY_ID
    aws_secret_access_key = YOUR_SECRET_ACCESS_KEY
    Save and Exit: Save the file and exit the text editor.

    Optional: Create ~/.aws/config File

You can also create a config file for additional configuration:

    Open the Config File:
    nano ~/.aws/config
Add Region and Output Format:
[default]
region = us-west-2  # Replace with your preferred region
output = json  # You can choose json, yaml, text, or table
Save and Exit.




    
