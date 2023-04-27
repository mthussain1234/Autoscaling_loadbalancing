# S3 buckets, EC2, Local Host
![image](https://user-images.githubusercontent.com/129314018/234845332-6c260967-a2d9-40c7-8504-1c0cb9371876.png)





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
11.  `aws configure` - configures aws cli, and when prompted enter AWS ACCESS KEY, SECRET ACCESS KEY, REGION AND OUTPUT FORMAT (secret key and access key should be found in your `.ssh` folder upon recieving)
12.  We enter our access and secret keys, and for region we enter `eu-west-1` and output format as `json`
13.  Once you enter, run `aws configure` to check if changes have been saved
14.  `aws s3 ls` - when running this it should show all objects in the S3 bucket, which should confirm AWS CLI has been configured correctly.
15.  We then use `aws s3 mb s3://nameofbucket` in the aws cli, name we used for name of bucket is `mohammad-tech221` use this naming convention
16.  Bucket should now be made and be present on the S3 interface on AWS -> navigating to buckets on the interface
17.  We make a test file using `sudo nano test.txt` and enter some information in it using `#`, save and exit
18.  We then use `aws s3 cp test.txt s3://mohammad-tech221`, to upload the file to our bucket
19.  Navigating through the S3 interface -> buckets -> <your-bucket>, it should show the file available within the bucket as shown below

![image](https://user-images.githubusercontent.com/129314018/234869105-4e211d9e-fe6b-4845-9f5c-adc280801a42.png)

