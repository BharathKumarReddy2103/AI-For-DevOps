**AI-Assisted Shell Scripting for DevOps:**

**Introduction**

In the evolving landscape of **DevOps**, automation plays a crucial role in simplifying workflows and reducing manual intervention. **Shell scripting** has long been a core skill for DevOps engineers, helping automate infrastructure tasks efficiently. With the advent of **AI-assisted development**, tools like **GitHub Copilot** are revolutionizing the way engineers write scripts.

In this guide, we'll explore how **AI-assisted shell scripting** can be leveraged to automate AWS infrastructure provisioning. Specifically, we'll use **GitHub Copilot** to generate a **Bash script** for creating an **AWS VPC with a public subnet**. We'll also discuss **best practices** for AI-assisted coding, security considerations, and an assignment to extend the script.

**Why AI-Assisted Shell Scripting?**

**The Role of AI in DevOps Automation**

Among the various tasks in **DevOps engineering**, AI can provide **significant benefits** when writing shell scripts. Unlike programming languages such as **Python or Terraform**, where AI-generated code may contain **deprecated packages** or **outdated APIs**, **shell scripting relies on Unix/Linux commands that have remained stable for decades.**

For example:

•	A **for loop** written in a shell script **10 years ago still works today.**

•	Commands like **grep, sed, awk, ls, pwd have backward compatibility.**

•	**No dependency issues** (unlike Python, where outdated modules may lead to security vulnerabilities).

**Benefits of AI-Assisted Shell Scripting**

✅ **Stable & Reliable** – Shell commands rarely change over time.

✅ **No Dependency Hell** – Unlike Python or Terraform, shell scripts don’t rely on external libraries that might become deprecated.

✅ **Automation at Scale** – AI can generate scripts quickly, reducing development time.

✅ **Improved Productivity** – AI pair programming helps engineers write cleaner and more efficient code.

**Getting Started with AI-Powered Shell Scripting**

**Installing GitHub Copilot for AI Pair Programming**

To leverage **AI assistance for shell scripting**, we will use **GitHub Copilot**:

**Steps to Install GitHub Copilot:**

**1.	Open Visual Studio Code (VS Code).**

**2.**	Navigate to the **Extensions tab**.

**3.	Search for "GitHub Copilot"** and click Install.

**4.	Enable GitHub Copilot** to assist with script writing.

Once installed, **Copilot** will **observe** your coding and suggest improvements in real time.

---

**Writing an AI-Generated Shell Script to Create an AWS VPC**

Now, let's write a **Bash script** to **create an AWS VPC and a public subnet.**

**Step 1: Define the Script Requirements**

Before we start writing the script, let’s define our requirements:

•	The script should **create a VPC** in AWS.

•	The script should **create a public subnet** inside the VPC.

•	The script should **verify if AWS CLI** is installed.

•	The script should **check if AWS credentials are configured.**

**Step 2: Writing the Shell Script Using GitHub Copilot**

Open **VS Code** and create a new file named:

```sh
aws_vpc_creation.sh
```

**Shell Script (Generated Using GitHub Copilot)**

```sh
#!/bin/bash

# Description: This script creates an AWS VPC with a public subnet.
# It verifies if AWS CLI is installed and configured before proceeding.

# Define Variables
VPC_CIDR="10.0.0.0/16"
SUBNET_CIDR="10.0.1.0/24"
REGION="us-east-1"
VPC_NAME="Demo-VPC"
SUBNET_NAME="Demo-Subnet"

# Check if AWS CLI is installed
if ! command -v aws &> /dev/null; then
    echo "AWS CLI is not installed. Please install AWS CLI before running this script."
    exit 1
fi

# Check if AWS CLI is configured
if ! aws sts get-caller-identity &> /dev/null; then
    echo "AWS CLI is not configured. Run 'aws configure' to set up credentials."
    exit 1
fi

# Create VPC
VPC_ID=$(aws ec2 create-vpc --cidr-block $VPC_CIDR --region $REGION --query "Vpc.VpcId" --output text)
echo "Created VPC with ID: $VPC_ID"

# Tag the VPC
aws ec2 create-tags --resources $VPC_ID --tags Key=Name,Value=$VPC_NAME

# Create Public Subnet
SUBNET_ID=$(aws ec2 create-subnet --vpc-id $VPC_ID --cidr-block $SUBNET_CIDR --region $REGION --query "Subnet.SubnetId" --output text)
echo "Created Subnet with ID: $SUBNET_ID"

# Tag the Subnet
aws ec2 create-tags --resources $SUBNET_ID --tags Key=Name,Value=$SUBNET_NAME

echo "AWS VPC and Public Subnet created successfully."
```

**Step 3: Running the Script**

**1.	Make the script executable:**

```sh
chmod +x aws_vpc_creation.sh
```

**2.	Run the script:**

```sh
./aws_vpc_creation.sh
```

**Expected Output**

```sh
Created VPC with ID: vpc-0a1b2c3d4e
Created Subnet with ID: subnet-0a1b2c3d4e
AWS VPC and Public Subnet created successfully.
```

---

**Best Practices for AI-Assisted Shell Scripting**

To **maximize AI-generated scripts' effectiveness**, follow these best practices:

**1. Use Meaningful File and Variable Names**

**•	Bad:** script.sh

**•	Good:** aws_vpc_creation.sh

**•	Bad:** var1=10.0.0.0/16

**•	Good:** VPC_CIDR="10.0.0.0/16"

**2. Provide Clear Descriptions in the Script**

•	Add a # Description at the top of the script to give AI more context.

**3. Verify AI-Generated Code**

•	Always **review AI-generated scripts** before executing.

•	If unsure, **ask Copilot to explain a specific line.**

**4. Use Error Handling**

•	Ensure the script **handles errors gracefully** to prevent unintended failures.

---

**Extending the Script: Assignment**

Now, let’s **extend** our script with an **additional feature:**

✅ **Modify the script to accept a command-line argument:**

•	If the user runs:

```sh
./aws_vpc_creation.sh create
```

 ✅ **Creates the VPC & Subnet.**
 
•	If the user runs:

```sh
./aws_vpc_creation.sh teardown
```

 ✅ **Deletes the VPC & Subnet.**
 
**Hint: Modify the script to include:**

```sh
if [ "$1" == "create" ]; then
   # Create VPC & Subnet
elif [ "$1" == "teardown" ]; then
   # Delete VPC & Subnet
else
   echo "Invalid argument. Use 'create' or 'teardown'."
fi
```

💡 **Challenge:** Implement the full script and test both creation and deletion functionality.

---

**Alternative AI Tools for Shell Scripting**

While **GitHub Copilot** is widely used, other AI tools can assist in **DevOps automation:**

| **AI Tool**       | **Best For**                          | **Free Plan?** |
|------------------|----------------------------------|------------|
| **GitHub Copilot** | Shell Scripting, Pair Programming | ✅ (Limited) |
| **Cursor AI**     | Terraform, Python, Advanced AI Pairing | ❌ (Paid) |
| **Tabnine**       | AI-powered Code Completion       | ✅ (Free Version) |

---

**Conclusion**

AI-assisted shell scripting is a **game-changer** for **DevOps engineers**. With tools like **GitHub Copilot**, you can **write automation scripts faster, minimize errors**, and **follow industry best practices.**

✅ **Start using AI pair programming today** and enhance your **DevOps automation skills**🚀

📌 **Want More?**

⭐ **Follow my GitHub for DevOps & Cloud content**

⭐ **Connect with me on LinkedIn**

**Happy Coding** 👨‍💻🚀
