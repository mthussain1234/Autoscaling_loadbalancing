# S3 buckets, EC2, Local Host
![image](https://user-images.githubusercontent.com/129314018/234845332-6c260967-a2d9-40c7-8504-1c0cb9371876.png)





# Setting up S3
Create a new EC2 instance, using Ubuntu 18.04, we used the naming convention `mohammad-s3-tech221`, and for security groups
add an SSH rule port 22 and `my-ip` to allow you to ssh in

1.  `sudo apt update -y` - updates package list
2.  `sudo apt upgrade -y` - upgrades installed packages to latest version
3.  `python --version` - python version currently installed
4.  `python3 --version` - version of python3 ins tall
5.  `sudo apt install python` - install python
6.  `sudo apt install python3-pip` - installs pip, package installer for python3
7.  `alias python=python3` - creates alias so python3 is used instead of python 
8.  `python --version` - should now show the python 3 version, after alias
9.  `sudo apt-get install python3-pip` - installs pip
10. `sudo python3 -m pip install awscli` - installs aws command line interface using pip
11. `aws configure` - configures aws cli, and when prompted enter AWS ACCESS KEY, SECRET ACCESS KEY, REGION AND OUTPUT FORMAT (secret key and access key should be found in your `.ssh` folder upon recieving)
12. We enter our access and secret keys, and for region we enter `eu-west-1` and output format as `json`
13. Once you enter, run `aws configure` to check if changes have been saved
14. `aws s3 ls` - when running this it should show all objects in the S3 bucket, which should confirm AWS CLI has been configured correctly.
15. We then use `aws s3 mb s3://nameofbucket` in the aws cli, name we used for name of bucket is `mohammad-tech221` use this naming convention
16. Bucket should now be made and be present on the S3 interface on AWS -> navigating to buckets on the interface
17. We make a test file using `sudo nano test.txt` and enter some information in it using `#`, save and exit
18. We then use `aws s3 cp test.txt s3://mohammad-tech221`, to upload the file to our bucket
19. Navigating through the S3 interface -> buckets -> <your-bucket>, it should show the file available within the bucket as shown below

![image](https://user-images.githubusercontent.com/129314018/234869105-4e211d9e-fe6b-4845-9f5c-adc280801a42.png)

20. If the file on local host is deleted (via `sudo rm test.txt`), we can use `aws s3 cp s3://bucket-name/filename filename`.
21. In our case it was `aws s3 cp s3://mohammad-tech221/test.txt test.txt`, once running this we can see the file was downloaded from the bucket again and after running `cat` we can see the contents are the same as before.

![image](https://user-images.githubusercontent.com/129314018/234872418-9564b26b-dbc4-4a7f-9497-bedeb1ab398a.png)
  
22. `aws s3 sync s3://bucket-name/ test.txt` - can also be used if there are a lot of files
23. `aws s3 rm s3://bucket-name/test.txt` - deletes object in the bucket, so the bucket is now empty, but the bucket itself is there
24. `aws s3 rb s3://bucket-name` - removes the bucket itself if empty, if not empty it would not allow you to delete
  
# S3 Python Scripting

1. Create new EC2 instance, using Ubuntu 18.04
2. From S3 steps, complete steps 1 - 10.
3. `sudo python3 -m install boto3` - 
4. Repeat steps 11-13 from the S3
5. Create a test file we make one with random text called `test_script.txt`
6. We then create 5 python scripts - `create_bucket.py`, `upload_file.py`, `download_file.py`, `delete_bucket_objects.py` and `delete_bucket.py`
7. For create_bucket the code is
```
import boto3

 

s3 = boto3.resource('s3')
s3.create_bucket(Bucket='mohammad-tech221-boto3', CreateBucketConfiguration= {'LocationConstraint': 'eu-west-1'})
```
8. Upload_file
```

import boto3

 

# Create an S3 client
s3_client = boto3.client('s3')

 

# Upload the file to S3
s3_client.upload_file("test_script.txt", "mohammad-tech221-boto3", "test_script.txt")
  
```
  
9. Download_file
```
import boto3

 

# Create an S3 client
s3_client = boto3.client('s3')

 

# Download the file from S3
s3_client.download_file("mohammad-tech221-boto3", "test_script.txt", "test_script.txt")
```
10. Delete_bucket_objects
```
import boto3

 

# Create an S3 resource
s3 = boto3.resource('s3')

 

# Delete all objects in the bucket
bucket = s3.Bucket('mohammad-tech221-boto3')
bucket.objects.all().delete()
```

11. Delete_bucket
```
import boto3

 

# Create an S3 resource
s3 = boto3.resource('s3')

 

# Delete all objects in the bucket
bucket = s3.Bucket('mohammad-tech221-boto3')
bucket.objects.all().delete()
```
12. To run the scripts, we use `python <py_script_name>.py`, and it should run the script needed, and should be reflected on the S3 interface.
13. Example of the `delete_bucket.py` function working is shown below.
  
  
![image](https://user-images.githubusercontent.com/129314018/234902939-2972eab1-7858-4cb7-9179-993c12d6977a.png)
