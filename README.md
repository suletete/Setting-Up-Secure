### **Mini Project - Setting Up Secure Authentication to AWS API**

In this mini project, you will set up secure authentication for AWS API using IAM roles, policies, and the AWS CLI. This setup will allow your scripts to interact with AWS resources, such as EC2 and S3, for automation purposes.

Here’s a detailed breakdown of the process:

---

### **Step 1: Create an IAM Role**

The IAM (Identity and Access Management) role defines the permissions your script will need to interact with AWS services. We will create a role that allows access to EC2 and S3 services.

1. **Login to AWS Management Console**:
   - Go to the AWS Management Console and log in.

2. **Navigate to IAM**:
   - In the search bar, type `IAM` and select **IAM** (Identity and Access Management).

3. **Create IAM Role**:
   - In the IAM dashboard, click **Roles** in the left pane.
   - Click **Create role**.
   - Choose **AWS service** for the trusted entity type and select **EC2**.
   - In the **Permissions policies** section, attach policies for EC2 and S3 access. You can use predefined policies like `AmazonEC2FullAccess` and `AmazonS3FullAccess`.
   - Provide a name for the role (e.g., `AutomationRole`).
   - Click **Create role**.

---

### **Step 2: Create an IAM Policy**

This policy specifies the exact permissions your script will require to access EC2 and S3.

1. **Create IAM Policy**:
   - Go to the **IAM Dashboard**.
   - Select **Policies** from the left sidebar and click **Create policy**.
   - Choose **JSON** and paste the following policy document:

   ```json
   {
     "Version": "2012-10-17",
     "Statement": [
       {
         "Effect": "Allow",
         "Action": [
           "ec2:*",
           "s3:*"
         ],
         "Resource": "*"
       }
     ]
   }
   ```

   This policy grants full access to EC2 and S3 resources.

2. **Attach Policy**:
   - Name the policy (e.g., `FullEC2S3AccessPolicy`) and click **Review policy**.
   - After reviewing, click **Create policy**.

---

### **Step 3: Create an IAM User**

Now, create an IAM user named `automation_user` that your script will use to access AWS resources.

1. **Create IAM User**:
   - Go to the **IAM Dashboard**, select **Users** from the sidebar, and click **Add user**.
   - Enter `automation_user` as the user name.
   - Select **Programmatic access** to give the user API access.
   - Click **Next: Permissions**.

2. **Assign Role and Policy**:
   - Select **Attach policies directly**.
   - Search for and select the `FullEC2S3AccessPolicy` policy created earlier.
   - Click **Next: Tags**, and then **Next: Review**.
   - Click **Create user**.

3. **Download Credentials**:
   - Save the **Access Key ID** and **Secret Access Key** displayed on the confirmation screen. These will be needed for configuring the AWS CLI.

---

### **Step 4: Assign User to IAM Role**

1. **Attach Role to User**:
   - Go to **IAM Dashboard**.
   - Under **Users**, click on `automation_user`.
   - In the **Permissions** tab, click **Add permissions**.
   - Select **Attach policies directly** and choose the `FullEC2S3AccessPolicy`.
   - Click **Review** and then **Add permissions**.

---

### **Step 5: Install and Configure the AWS CLI**

Once IAM roles and policies are in place, install the AWS CLI to interact with AWS via the terminal.

#### **Installing AWS CLI**

**On Linux**:

1. **Download AWS CLI**:

   ```bash
   curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
   ```

2. **Unzip the installer**:

   ```bash
   unzip awscliv2.zip
   ```

3. **Run the installer**:

   ```bash
   sudo ./aws/install
   ```

**On Windows**:
- Visit [AWS CLI v2 download page](https://aws.amazon.com/cli/) and download the MSI installer.
- Follow the installation wizard steps to complete.

**On macOS**:
- Download the `.pkg` installer from AWS CLI website.
- Run the installer and follow the on-screen steps.

#### **Configuring AWS CLI**

1. **Configure AWS CLI**:
   After installation, configure the AWS CLI using the access credentials for `automation_user`.

   Open the terminal or Command Prompt and run:

   ```bash
   aws configure
   ```

2. **Enter Your Credentials**:
   - When prompted, enter the **Access Key ID** and **Secret Access Key** generated for `automation_user`.
   - Specify the **Default region name** (e.g., `us-east-1`).
   - Choose the **Default output format** (e.g., `json`).

---

### **Step 6: Test AWS CLI Configuration**

1. **Verify CLI Configuration**:
   To check if the AWS CLI is properly configured, you can run a basic command like:

   ```bash
   aws ec2 describe-regions --output table
   ```

   This command will list all available EC2 regions and display them in a table format. If it works, your CLI is set up correctly and ready to make API calls to AWS.

---

### **Understanding APIs**

An **API (Application Programming Interface)** is a set of protocols and tools that allows software applications to communicate with each other. In this case, the **AWS API** allows you to interact programmatically with AWS services. By using the AWS CLI or SDKs, you can make requests (API calls) to create, modify, or delete AWS resources like EC2 instances and S3 buckets.

---

### **Final Thoughts**

Once you have completed this mini project, you will have successfully set up secure authentication to the AWS API using IAM roles, policies, and the AWS CLI. This will allow you to automate the creation and management of AWS resources via your script, streamlining your cloud operations.
