# Capstone Project - Introduction to Cloud Computing 

## Capstone Project: E-Commerce Platform Deployment with Git, Linux and AWS. 

### Abstract
This capstone project focuses on deploying a static e-commerce website using Git, Linux, and AWS. It demonstrates proficiency in version control, cloud computing, and web server configuration. The project follows a structured approach, including repository setup, website deployment, and continuous integration for updates. The final implementation ensures a scalable and accessible web presence hosted on AWS.

### Description
This project demonstrates the skills and knowledge I have acquired in setting up and deploying a static website using Git, Linux, and AWS. It showcases my ability to implement version control through Git, manage a structured development workflow, and deploy applications in a cloud environment. The project involves creating and managing branches, staging, committing, and pushing changes to a remote repository, as well as configuring and hosting the website on an AWS EC2 instance. Detailed snapshots of the commands executed and tasks performed are included for documentation and transparency. This capstone project reinforces my expertise in Git operations, Linux server management, and cloud deployment, key skills essential for modern DevOps practices.

### Objectives
* Implement version control using Git.
* Host a static e-commerce website on AWS EC2.
* Automate deployments using Git workflows.
* Secure and optimize the server configuration for better performance.

### Tools and Technologies Used
* Version Control: Git, GitHub
* Cloud Services: AWS EC2
* Operating System: Linux (Ubuntu/CentOS)
* Web Server: Apache
* Development Tools: CLI, SSH
* Programming Languages: HTML, CSS, JavaScript (if applicable)

#### Tasks 1: Implement Version Control with Git
#### 1.1. Initialize Git Repository
A project directory was created and named MarkPeak_Ecommerce. After navigating into this directory via the macOS terminal, the **git init** command was executed to initialize a Git repository.

#### 1.2. Obtain and Prepare the E-Commerce Website Template
Since building the website code from scratch was unnecessary, a pre-existing e-commerce template was downloaded.

* Downloading a Template:
A suitable template was sourced from Tooplate. (Tooplate)[https://www.tooplate.com/]  
![Waso Strategy](https://github.com/Samjean50/MarkPeak_Ecommerce/blob/main/images/dowload-the%20template.png)

* Preparing the Template:
The ZIP file was extracted using the **unzip** command. Its contents were then copied to the MarkPeak_Ecommerce project folder using the **cp filename/path/to/folder** command.

#### 1.3. Stage and Commit the Template to Git
Git global configuration settings for username and email were applied with the following commands:

```lua
git config --global user.name
git config --global user.email
```

Website files were staged and committed with:

```sql
git add .
git commit -m "Initial commit with basic e-commerce site structure"
```

#### 1.4. Push the Code to GitHub
To enable version control and collaboration, the local project was pushed to a remote repository.

* Create the Remote Repository:
On GitHub, a new repository named MarketPeak_Ecommerce was created without initializing it with a README, .gitignore, or license.

* Link Local Repository:
The remote URL was added with:

```csharp
git remote add origin https://github.com/Samjean50/MarketPeak_Ecommerce.git
```

* Push the Code:

```css
git push -u origin main
```
![push](https://github.com/Samjean50/MarkPeak_Ecommerce/blob/main/images/ecom%20push.png)

#### Tasks 2: AWS Deployment
#### 2.1. Set Up an AWS EC2 Instance
An EC2 instance was launched via the AWS Management Console using the Amazon Linux AMI. A new security group and key pair were generated, and connection to the instance was established via SSH.

#### 2.2. Clone the Repository on the EC2 Instance
Before deployment, the repository was cloned to the instance.

* Authentication via SSH:
An SSH key pair was generated using **ssh-keygen**, and the public key was retrieved with:

```bash
cat /home/ec2-user/.ssh/id_rsa.pub
```
This key was added to GitHub, enabling secure cloning:

```scss
git clone git@github.com:Samjean50/MarketPeak_Ecommerce.git
```

* Authentication via HTTPS (Alternative):

If SSH was not configured, cloning via HTTPS was also an option:

```bash
git clone https://github.com/Samjean50/MarketPeak_Ecommerce.git
```
* Install Git (if not preinstalled):
On Amazon Linux, Git was installed using:

```nginx
sudo yum install git
```


#### 2.3. Install Apache Web Server on EC2
Apache (httpd) was installed and configured to host the website:

```pgsql
sudo yum update -y
sudo yum install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd
```
#### 2.4. Configure Apache for the Website
* Prepare the Web Directory:
The default Apache web directory contents were cleared:

```bash
sudo rm -rf /var/www/html/*
```
Website files from the cloned repository were copied into the directory:

```ruby
sudo cp -r ~/MarketPeak_Ecommerce/2130_waso_strategy/* /var/www/html/
```
* Reload Apache:

```nginx
sudo systemctl reload httpd
```

#### 2.5. Access the Website in a Browser
The website became accessible via the EC2 instance’s public IP (http://52.207.115.56/).

Note: Initially, the site did not load because port 80 was not open in the security group. This was resolved by editing the inbound rules and enabling HTTP traffic.
![Final site](https://github.com/Samjean50/MarkPeak_Ecommerce/blob/main/images/final-site.png)

#### Tasks 3: Continuous Integration and Deployment Workflow
A structured workflow was followed to support smooth development, testing, and deployment.

#### Step 1: Develop New Features and Fixes
* Create a Development Branch:

```nginx
git branch development
git checkout development
```
* Implement Changes:
New features or bug fixes were added on the development branch. In this case, a new file was introduced.

#### Step 2: Version Control with Git
Changes were staged and committed, then pushed to the development branch:

```sql
git add .
git commit -m "Add new features or fix bugs"
git push origin development
```
#### Step 3: Pull Requests and Merging to Main
* Create a Pull Request:
On GitHub, a pull request was opened to merge the development branch into the main branch.
![pull-request](https://github.com/Samjean50/MarkPeak_Ecommerce/blob/main/images/pull-request.png)

* Review and Merge:

```css
git checkout main
git merge development
```

![gitmerge](https://github.com/Samjean50/MarkPeak_Ecommerce/blob/main/images/github-merge.png)

* Push Merged Changes to GitHub:

```css
git pull
git push origin main
```
![syncing](https://github.com/Samjean50/MarkPeak_Ecommerce/blob/main/images/ecom%20push.png)

#### Step 4: Deploy Updates to Production
* Pull Latest Code on EC2:

```css
git pull origin main
```

* Restart Apache (if needed):

```nginx
sudo systemctl reload httpd
```

#### Step 5: Test Live Changes
The updated e-commerce website was accessed via browser to confirm new features and fixes were functioning correctly.

http://52.207.115.56/2130_waso_strategy/


