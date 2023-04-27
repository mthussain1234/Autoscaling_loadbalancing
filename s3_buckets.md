# Setting up S3
Create a new EC2 instance, using Ubuntu 18.04, we used the naming convention `mohammad-s3-tech221`, and for security groups
add an SSH rule port 22 and `my-ip` to allow you to ssh in

1.   `sudo apt update -y` - updates package list
2.   `sudo apt upgrade -y` - upgrades installed packages to latest version
3.   `python --version` - python version currently installed
4.   `python3 --version` - version of python3 ins tall
5.   `sudo apt install python` - install python
6.   `sudo apt install python3-pip` - installs pip, package installer for python3
7.   `alias python=python3` - creates alias so python3 is used instead of python 
8.  `python --version` - should now show the python 3 version, after alias
9.  `sudo apt-get install python3-pip` - installs pip
10.  `sudo python3 -m pip install awscli` - installs aws command line interface using pip
11.  `aws configure` - configures aws cli, and when prompted enter AWS ACCESS KEY, SECRET ACCESS KEY, REGION AND OUTPUT FORMAT
12.  We enter our access and secret keys, and for region we enter `eu-west-1` and output format as `json`
13.  Once you enter, run `aws configure` to check if changes have been saved
14.  `aws s3 ls` - when running this it should show all objects in the S3 bucket, which should confirm AWS CLI has been configured correctly.
