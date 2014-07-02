Deploying a Flask Application to AWS Elastic Beanstalk
===============
Simple Python and Flask sample application from [AWS Elastic Beanstalk Developer Guide](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/create_deploy_Python_flask.html)


This section walks you through deploying a sample application to AWS Elastic Beanstalk using eb (an updated command line interface) and Git, and then updating the application to use the Flask framework. The following frameworks have been tested with AWS Elastic Beanstalk:

- Flask 0.9
- Flask 0.8

Step 1: Initialize Your Git Repository
------
Eb is a command line interface that enables you to deploy applications quickly and more easily using Git. Eb is available as part of the Elastic Beanstalk command line tools package. Follow the steps below to install eb and initialize your Git repository.

To install eb, its prerequisite software, and initialize your Git repository

1. Install the following software onto your local computer:

  1. Linux/Unix/MAC

    - Download and unzip the Elastic Beanstalk command line tools package at the AWS Sample Code & Libraries website. You can install either version 2.6.0 or version 2.6.1 of the AWS DevTools. Version 2.6.0 uses Ruby. Version 2.6.1 uses Python.

    - Git 1.6.6 or later. To download Git, go to http://git-scm.com/.

    - Ruby version 1.8.7 or later. To view and download Ruby clients, go to http://www.ruby-lang.org/en/.

    - Python 2.7 or 3.0.

  2. Windows

    - Download and unzip the Elastic Beanstalk command line tools package at the AWS Sample Code & Libraries website.

    - Git 1.6.6 or later. To download Git, go to http://git-scm.com/.

    - PowerShell 2.0.

        Note:  Windows 7 and Windows Server 2008 R2 come with PowerShell 2.0. If you are running an earlier version of Windows, you can download PowerShell 2.0. Visit http://technet.microsoft.com/en-us/scriptcenter/dd742419.aspx for more details.

2. Initialize your Git repository.
