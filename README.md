# Capstone Project - Introduction to Cloud Computing 

## Capstone Project: E-Commerce Platform Deployment with Git, Linux and AWS. 

### Project Instructions:

In this project i will be developing an e-commerce website for a new online marketplace named "MarketPeak." This platform will feature product listings, a shopping cart and user authentication. To carry out this project, i will utilize Git for version control, develop the website in a Linux environment, and deploy it on on AWS instance.

#### Tasks 1: Implement Version Control with Git
#### Implement Version Control with Git

#### 1.1. Initialize Git Repository:
I created the project directory and named it "MarkPeak_Ecommerce. then cd into the new project directory and ran the **git init** command to make it a git repository.

Note: I used the terminal on my MAC-OS to execute these commands.

#### 1.2. Obtain and Prepare the E-Commerce Website Template:
 I downloaded a pre-existing e-commerce website template as i dont have to develop the website code.

* To download a Website Template: 
 I visited (Tooplate)[https://www.tooplate.com/] or any other free template resource, and download a suitable e-commerce website template. 
![Waso Strategy](https://github.com/Samjean50/MarkPeak_Ecommerce/blob/main/images/dowload-the%20template.png)

* Prepare the Website Template:
 I extracted the downloaded template into your project directory, MarketPeak_Ecommerce.

 Note: I unzipped the file using the **unzip** command and i used cp filename/path/to/folder to copy the unzipped file to MarkDown_Ecommerce folder.

#### 1.3. Stage and Commit the Template to Git:

I carried out the folowing actions

**git config --global user.name**

**git config --global user.email**

**git commit -m "Initial commit with basic e-commerce site structure"**

Note : I set the Git global configuration of my username and email using the above commands and committed my changes with a clear descriptive message. Then  i added the website files to the Git repository using the **git add .** command.

#### 1.4. Push the code to your Github repository

To have a backup of all our website files i pushed all the files added to a remote git repository, this is crucial for version control and collaboration.

* Create a Remote Repository on GitHub:

I logged in into your GitHub account and created a new repository named "MarketPeak_Ecommerce" Leave the repository empty without initializing it with a README, .gitignore, or license.**

* Link Your Local Repository to GitHub:
In my terminal, the project directory, i added the remote repository URL to my local repository configuration.

**git remote add origin https://github.com/Samjean50/MarketPeak_Ecommerce.git**

* Push your code to GitHub repository: 
I pushed using the following command:

**git push -u origin main**
code-pushed

#### Tasks 2: AWS Deployment
 #### 2.1. Set Up an AWS EC2 Instance

* Log in to the AWS Management Console.
* Launch an EC2 instance using an Amazon Linux AMI.
* Connect to the instance using SSH.

Note: When setting up my instance, i created a new security group and a new key pair. 


 #### 2.2. Clone the repository on the Linux Server

Before deploting the e-commerce platform i cloned the GitHub repository to your AWS EC2 instance. This process involves authenticating with GitHub and choosing between two primary methods of cloning a repository: SSH and HTTPS.

* Authenticating with GitHub using ssh

On my EC2 instance, i generated a SSH keypair using **ssh-keygen** 

* cat and copy the public key.

**cat /home/ec2-user/.ssh/id_rsa.pub
sshkey-copied**

* Added ssh public key to GitHub repository:

I created a ssh key in my github repository

ssh-link

**git clone git@github.com:Samjean50/MarketPeak_Ecommerce.git** 

* Authenticating with GitHub using HTTPS

For repositories that you plan to clone without setting up SSH keys, use the HTTPS URL. GitHub will prompt for your username and password:

https-link

git clone https://github.com/Samjean50/MarketPeak_Ecommerce.git

Note: With Amazon Linux, git is not preinistalled so I had to manually install it manually, using the following command:

**sudo yum install git**

#### 2.3. Installing a Web Server on EC2

Apache HTTP Server (httpd) is a widely used web server that serves HTML files and content over the internet. Installing it on Linux EC2 server allows you to host MarketPeak E-commerce site:

* Install Apache web server on the EC2 instance: 

I used the following command to install Apache:
**sudo yum update -y**

**sudo yum install httpd -y**

**sudo systemctl start httpd**

**sudo systemctl enable httpd**

#### 2.4. Configure httpd for Website:

Prepare the Web Directory: I cleared the default httpd web directory and copied MarketPeak Ecommerce website files to it.

**sudo rm -rf /var/www/html/***  # Delete the default

**sudo cp -r ~/MarketPeak_Ecommerce/2130_waso_strategy/*** /var/www/html/ # copy the content of MarketPeak_Ecommerce cloned earlier

Reload httpd: Applied the changes by reloading the httpd service.
**sudo systemctl reload httpd**


#### 2.5.  Access Website from Browser 
With httpd configured and website files in place, MarketPeak Ecommerce platform is now live on the internet: Open a web browser and access the public IP (http://52.207.115.56/) of your EC2 instance to view the deployed website.

Note: When i initially created my security group, i didnt open my port 80 so the website didnt load/respond at first when i used the public IP address of the instance. Then i realized my mistake and i went to edit the inbound rules of my security group and opened port 80 then the website responded using the same public IP adddress of my instance. 
![Final site](https://github.com/Samjean50/MarkPeak_Ecommerce/blob/main/images/final-site.png)


#### Tasks 3: Continuous Integration and Deployment Workflow
To ensure a smooth workflow for developing, testing, and deploying my e-commerce platform, i follow this structured approach. It covers making changes in a development environment, utilizing version control with Git, and deploying updates to your production server on AWS.

#### Step 1:
Developing New Features and Fixes

* Created a Development Branch: I created a separate branch using the commands below. This isolates new features and bug fixes from the stable version of your website. 

**git branch development**
**git checkout development**
**development-branch**

* Implement Changes: On the development branch, i added new features or bug fixes. I only created a new file on the development branch

#### Step 2: 
Version control with Git

ran the the following git command to stage, commit, and push to development branch:

**git add .**

**git commit -m "Add new features or fix bugs"**

**git push origin development**


#### Step 3:
Pull Requests and Merging to the Main branch

* Create a Pull Request (PR): On GitHub, i created a pull request to merge the development branch into the main branch. This process is crucial for code review and maintaining code quality.
![pull-request](https://github.com/Samjean50/MarkPeak_Ecommerce/blob/main/images/pull-request.png)

* Review and Merge the PR: Reviewed the changes for any potential issues. Once satisfied,i merged the pull request into the main branch, incorporating the new features or fixes into the production codebase.
[githubmerge]: https://github.com/Samjean50/MarkPeak_Ecommerce/blob/main/images/github-merge.png

**git checkout main**
**git merge development**
![gitmerge] (https://github.com/Samjean50/MarkPeak_Ecommerce/blob/main/images/git-merge.png)

* Push the Merged Changes to GitHub: Ensure that your local main branch, now containing the updates, is pushed to the remote repository on GitHub.

**git pull**
**git push origin main**

![syncing] (https://github.com/Samjean50/MarkPeak_Ecommerce/blob/main/images/synching-local-and-remote-main.png)

#### Step 4: Deploying Updates to the Production Server
|* Pull the Latest Changes on the Server: SSH into your AWS EC2 instance where the production website is hosted. I navigated to the website's directory and pull the latest changes from the main branch using the command below.

**git pull origin main**
* Restart the Web Server (if necessary): Depending on the nature of the updates, I restarted the web server to apply the changes.

**sudo systemctl reload httpd**

#### Step 5: Testing the New Changes

* Access the Website: Open a web browser and navigate to the public IP address of your EC2 instance. Test the new features or fixes to ensure they work as expected in the live environment.

This workflow emphasizes best practices in software development and deployment, including branch management, code review through pull requests, and continuous integration/deployment strategies. By following these steps, you maintain a stable and up-to-date production environment for your e-commerce platform.

http://52.207.115.56/2130_waso_strategy/

