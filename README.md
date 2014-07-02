Deploying a Flask Application to AWS Elastic Beanstalk
------
Simple Python and Flask sample application from [AWS Elastic Beanstalk Developer Guide](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/create_deploy_Python_flask.html)


This section walks you through deploying a sample application to AWS Elastic Beanstalk using eb (an updated command line interface) and Git, and then updating the application to use the Flask framework. The following frameworks have been tested with AWS Elastic Beanstalk:

- Flask 0.9
- Flask 0.8

###Step 1: Initialize Your Git Repository
Eb is a command line interface that enables you to deploy applications quickly and more easily using Git. Eb is available as part of the Elastic Beanstalk command line tools package. Follow the steps below to install eb and initialize your Git repository.
####To install eb, its prerequisite software, and initialize your Git repository
1. Install the following software onto your local computer:

  a. Linux/Unix/MAC
    - Download and unzip the Elastic Beanstalk command line tools package at the [AWS Sample Code & Libraries website](http://aws.amazon.com/code/6752709412171743). You can install either version 2.6.0 or version 2.6.1 of the AWS DevTools. Version 2.6.0 uses Ruby. Version 2.6.1 uses Python.
    - Git 1.6.6 or later. To download Git, go to http://git-scm.com/.
    - Ruby version 1.8.7 or later. To view and download Ruby clients, go to http://www.ruby-lang.org/en/.
    - Python 2.7 or 3.0.
  
  b. Windows
    - Download and unzip the Elastic Beanstalk command line tools package at the [AWS Sample Code & Libraries website](http://aws.amazon.com/code/6752709412171743).
    - Git 1.6.6 or later. To download Git, go to http://git-scm.com/.
    - PowerShell 2.0.
    *Note:  Windows 7 and Windows Server 2008 R2 come with PowerShell 2.0. If you are running an earlier version of Windows, you can download PowerShell 2.0. Visit http://technet.microsoft.com/en-us/scriptcenter/dd742419.aspx for more details.*

2. Initialize your Git repository.
  
  ```bash
  git init .
  ```

###Step 2: Configure AWS Elastic Beanstalk

You use eb, a command line tool, to configure AWS Elastic Beanstalk. If you haven't already installed eb on your local computer, do that now at the [AWS Sample Code & Libraries website](http://aws.amazon.com/code/6752709412171743). If you are running eb on a Linux operating system, you will need to install Python 2.7 or 3.0.

Before you use eb, set your PATH to the location of eb. The following table shows an example for Linux/UNIX and Windows.

On Linux and UNIX	| On Windows
--- | ---
```$ export PATH=$PATH:<path to unzipped EB CLI package>/eb/linux/python2.7/``` |	```C:\> set PATH=%PATH%;<path to unzipped EB CLI package>\eb\windows\```
Use the init command, and AWS Elastic Beanstalk will prompt you to enter this information. If a default value is available, and you want to use it, press Enter.

####To configure AWS Elastic Beanstalk

1. From your directory where you created your local repository, type the following command.

  ```bash
  eb init
  ```

2. When you are prompted for the access key ID, type your access key ID. To get your access key ID, see [How Do I Get Security Credentials?](http://docs.aws.amazon.com/general/latest/gr/getting-aws-sec-creds.html) in the AWS General Reference.

  ```bash
  Enter your AWS Access Key ID (current value is "AKIAIOSFODNN7EXAMPLE"): 
  ```

3. When you are prompted for the secret access key, type your secret access key. To get your secret access key, see [How Do I Get Security Credentials?](http://docs.aws.amazon.com/general/latest/gr/getting-aws-sec-creds.html) in the AWS General Reference.

  ```bash
  Enter your AWS Secret Access Key (current value is "wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY"): 
  ```

4. When you are prompted for the AWS Elastic Beanstalk region, type the number of the region. For information about this product's regions, go to [Regions and Endpoints](http://docs.aws.amazon.com/general/latest/gr/rande.html?r=1166) in the Amazon Web Services General Reference. For this example, we'll use US East (Virginia).

5. When you are prompted for the AWS Elastic Beanstalk application name, type the name of the application. AWS Elastic Beanstalk autogenerates an application name based on the current directory name if an application name has not been previously configured. In this example, we use flaskapp.

  ```bash
  Enter an AWS Elastic Beanstalk application name (auto-generated value is "windows"): flaskapp
  ```
  *Note:  If you have a space in your application name, make sure you do not use quotes.*

6. When you are prompted for the AWS Elastic Beanstalk environment name, type the name of the environment. AWS Elastic Beanstalk automatically creates an environment name based on your application name. If you want to accept the default, press Enter.

  ```bash
  Enter an AWS Elastic Beanstalk environment name (current value is "flaskapp-env"): 
  ```
  *Note:  If you have a space in your application name, make sure you do not have a space in your environment name.*

7. When you are prompted, choose an environment tier. For this example, we'll use 1. For more information about environment tiers, see [Architectural Overview](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/concepts.concepts.architecture.html).

  ```bash
  Available environment tiers are:
  1) WebServer::Standard::1.0
  2) Worker::SQS/HTTP::1.0
  ```
  
8. When you are prompted for the solution stack, type the number of the solution stack you want. For more information about solution stacks, see [Supported Platforms](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/concepts.platforms.html). For this example, we'll use 32bit Amazon Linux 2013.09 running Python.

9. When you are prompted, choose an environment type.

  ```bash
  Available environment types are: 
  1) LoadBalanced
  2) SingleInstance
  ```
  
10. When you are prompted to create an Amazon RDS database, type y or n. For more information about using Amazon RDS, see [Using AWS Elastic Beanstalk with Amazon RDS](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/AWSHowTo.RDS.html). For this example, we'll type n.

  ```bash
  Create RDS instance? [y/n]: n
  ```

11. When you are prompted to enter your instance profile name, you can choose to create a default instance profile or use an existing instance profile. Using an instance profile enables IAM users and AWS services to gain access to temporary security credentials to make AWS API calls. Using instance profiles prevents you from having to store long-term security credentials on the EC2 instance. For more information about instance profiles, see [Granting Permissions to Users and Services Using IAM Roles](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/AWSHowTo.iam.html#AWSHowTo.iam.roles). For this example, we'll use Create a default instance profile.

After configuring AWS Elastic Beanstalk, you are ready to deploy a sample application.

If you want to update your AWS Elastic Beanstalk configuration, you can use the init command again. When prompted, you can update your configuration options. If you want to keep any previous settings, press the Enter key.

###Step 3: Create Application

Next, you need to create and deploy a sample application. In these procedures, you use a sample application that is already prepared. AWS Elastic Beanstalk uses the configuration information you specified in the previous step to do the following:

  - Create an application using the application name you specified.
  - Launch an environment using the environment name you specified that provisions the AWS resources to host the application.
  - Deploy the application into the newly created environment.

Use the start command to create and deploy a sample application.

####To create the application

  - From your directory where you created your local repository, type the following command.

  ```bash
  eb start
  ```
  
This process may take several minutes to complete. AWS Elastic Beanstalk will provide status updates during the process. If at any time you want to stop polling for status updates, press Ctrl+C. Once the environment status is Green, AWS Elastic Beanstalk will output a URL for the application.

###Step 4: View Application

In the previous step, you created an application and deployed it to AWS Elastic Beanstalk. After the environment is ready and its status is Green, AWS Elastic Beanstalk provides a URL to view the application. In this step, you can check the status of the environment to make sure it is set to Green and then copy and paste the URL to view the application.

Use the status command to check the environment status, and then use the URL to view the application.

####To view the application

1. From your directory where you created your local repository, type the following command.

  ```bash
  eb status --verbose
  ```
  AWS Elastic Beanstalk displays the environment status. If the environment is set to Green, AWS Elastic Beanstalk displays the URL for the application. If you attached an RDS DB instance to your environment, your RDS DB information is displayed.

2. Copy and paste the URL into your web browser to view your application.

###Step 5: Update Application

After you have deployed a sample application, you can update the sample application with your own application. In this step, we'll update the sample application with a simple "Hello World" Flask application.

####To update the sample application

1. On your local computer, create a requirements.txt file.

  ```bash
  Flask==0.9
  ```
  *Note:  For more information about the requirements file, go to [Requirements files](http://www.pip-installer.org/en/latest/cookbook.html#requirements-files).
On your local computer, create an application.py file.*

  ```python
  import flask
 
  application = flask.Flask(__name__)

  #Set application.debug=true to enable tracebacks on Beanstalk log output. 
  #Make sure to remove this line before deploying to production.
  application.debug=True
 
  @application.route('/')
  def hello_world():
      return "Hello world!"
 
  if __name__ == '__main__':
      application.run(host='0.0.0.0', debug=True)
  ```    
  
2. Add your two files to your local Git repository, and then commit your change.

  ```bash
  git add .
  git commit -m "update app"
  ```
  *Note:  For information about Git commands, go to [Git - Fast Version Control System](http://git-scm.com/).
Create an application version matching your local repository and deploy to the Elastic Beanstalk environment if specified.*

  ```bash
  git aws.push
  ```

  You can also configure Git to push from a specific branch to a specific environment. For more information, see [Deploying a Git Branch to a Specific Environment](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/command-reference-branch-environment.html).

5. Refresh your web browser to view your updated application when your environment is ready.

You can access the logs for your EC2 instances running your application. For instructions on accessing your logs, see [Working with Logs](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/using-features.loggingS3.title.html).

###Step 6: Clean Up

If you no longer want to run your application, you can clean up by terminating your environment and deleting your application.

Use the stop command to terminate your environment and the delete command to delete your application.

####To delete the application

1. From your directory where you created your local repository, type the following command.

  ```bash
  eb stop
  ```
  This process may take a few minutes. AWS Elastic Beanstalk will display a message once the environment has been successfully terminated.
  *Note:  If you attached an RDS DB instance to your environment, your RDS DB will be deleted, and you will lose your data. To save your data, create a snapshot before you delete the application. For instructions on how to create a snapshot, go to [Creating a DB Snapshot](http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_CreateSnapshot.html) in the Amazon Relational Database Service User Guide.*

2. From your directory where you installed the command line interface, type the following command.

  ```bash
  eb delete
  ```

AWS Elastic Beanstalk will display a message once it has successfully deleted the application.
