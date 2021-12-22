---
title: AWS EC2 Instruction
date: 2020-10-22
permalink: /posts/2020/10-AWS-EC2-setting
excerpt_separator: <!--more-->
toc: true
tags:
  - aws
---

**Step 0: Install PuTTY in windows**

PuTTY is a free implementation of SSH for Windows. You can download the PuTTY installer from the following link: [https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)

![](/images/posts/AWS-setting/Image1.png)

Choose the version you need for your windows system accordingly.

**Step 1: Login in Amazon AWS and launch an EC2 instance.**

After you login your account, open the services and go to EC2 dashboard.

<!--more-->

![](/images/posts/AWS-setting/Image2.png)

Click &quot;Launch instance&quot; under the drawer of &quot;Launch instance&quot;.

![](/images/posts/AWS-setting/Image3.png)

Select &quot;**Amazon Linux AMI 2018.03.0 (HVM), SSD Volume Type** - ami-027cab9a7bf0155df&quot; as Amazon Machine Image (AMI).

![](/images/posts/AWS-setting/Image4.png)

Select &quot;r5d.large&quot; as your instance type and then click &quot;Next: Configure Instance Details&quot;.

![](/images/posts/AWS-setting/Image5.png)

Don&#39;t change any setting and click &quot;Next: Add storage&quot;.

![](/images/posts/AWS-setting/Image6.png)

Click &quot;Next: Add Tags

![](/images/posts/AWS-setting/Image7.png)

dg

![](/images/posts/AWS-setting/Image8.png)

Move to next page and click &quot;Launch&quot;. Choose &quot;Create a new key pair&quot; and give a key pair name in the pop-up window.

![](/images/posts/AWS-setting/Image9.png)

And then click &quot;Download Key Pair&quot;. Please keep your key pair in a safe place. It will be used to connect to EC2 from the local machine. After you download the file, click &quot; Launch Instances&quot;.

![](/images/posts/AWS-setting/Image10.png)

Now you have launched EC2 instance.

**Step 2: Convert public key to private key**

Open PuTTY Key Generator and click &quot;Load&quot; to locate the key pair file you download. And then click &quot;Save private key&quot;.

![](/images/posts/AWS-setting/Image11.png)

**Step 3: Connect to EC2 from local**

Go to EC2 dashboard and check running instances. Copy &quot;Public IPv4 DNS&quot;.

![](/images/posts/AWS-setting/Image12.png)

Open PuTTY. At blank of host name, type &quot;ec2-user@&quot; and paste the address you just get.

![](/images/posts/AWS-setting/Image13.png)

In the **Category** pane, choose **Connection** , **SSH** and **Auth**. Complete the following:

- Choose **Browse** , select the .ppk file that you generated for your key pair, and then choose **Open**.
- Choose **Open** to start the PuTTY session.

![](/images/posts/AWS-setting/Image14.png)

So now you can connect to EC2 instance from local.

![](/images/posts/AWS-setting/Image15.png)

**Step 4 AWS configuration**

Run this command to quickly set and view your credential, region and output format. The following example show sample values.

![](/images/posts/AWS-setting/Image16.png)

Replace AWS access key id and AWS secret access key to your own ones.

**Step 5 Install Python 3, pip 3, and the EB CLI on instance**

In Linux command line, type as shown in the figure.

```sh
[ec2-user@ip-172-31-15-113 ~] $ sudo yum install python36
```

Type &quot;y&quot; and click enter.

![](/images/posts/AWS-setting/Image18.png)

Install pip for python 3. Download the installation script.

```sh
[ec2-user@ip-172-31-15-113 ~] $ curl -O https://bootstrap.pypa.io/get-pip.py
```

Run the script with Python.

```sh
[ec2-user@ip-172-31-15-113 ~] $ python3 get-pip.py --user
```

Use pip to install the EV CLI

```sh
[ec2-user@ip-172-31-15-113 ~] $ pip3 install awsebcli --upgrade --user
```

**Step 6 Install Python packages for the project**

```sh
[ec2-user@ip-172-31-15-113 ~] $ pip3 install tweepy
[ec2-user@ip-172-31-15-113 ~] $ pip3 install pandas
```
You can check if the packages are installed successfully through the command:

```sh
[ec2-user@ip-172-31-15-113 ~] $ pip show pandas
```

**Step 7 Load files into EC2 instance**

Use the following command to copy an object from Amazon S3 to your instance.

[ec2-user ~]$ aws s3 cp s3://my\_bucket/my\_folder/my\_file.ext my\_copied\_file.ext

Eg:

```sh
[ec2-user@ip-172-31-15-113 ~] $ aws s3 cp s3://bucket1/hate_5000-1.csv hate_5000-1.csv
```

Use the same method to load python program &quot;Tweets\_scraper.py&quot; into EC2 instance.

Make sure both data and python program are in instance already using the command below.

![](/images/posts/AWS-setting/Image25.png)

**Step 8 change data file name and output file name in the python code and add your Twitter API token into the code.**

```sh
[ec2-user@ip-172-31-15-113 ~] $ nano Tweets_scraper.py
```

Change the load file name to the one you copy to EC2 instance. Add your consumer key, consumer secret, access token and access token secret into the code.

This link is for how to get API Keys and Tokens for Twitter: [https://www.slickremix.com/docs/how-to-get-api-keys-and-tokens-for-twitter/](https://www.slickremix.com/docs/how-to-get-api-keys-and-tokens-for-twitter/)

![](/images/posts/AWS-setting/Image27.png)

Change the output file name accordingly. If &#39; **hate\_5000-1.csv**&quot; is your input file, your output file name should be &quot; **hate\_5000-1-result.csv**&quot;. Use PgDn to move to the bottom of the code.

![](/images/posts/AWS-setting/Image28.png)

After these, press Ctrl+X, y and Enter in order.

![](/images/posts/AWS-setting/Image29.png)

**Step 9 Run the python program**

```sh
[ec2-user@ip-172-31-15-113 ~] $ python3 Tweets_scraper.py
```

**Step 10 Save your output file into S3 storage.**

Use the command to save file into S3 storage.

```sh
[ec2-user@ip-172-31-15-113 ~] $ aws s3 cp hate_5000-1-result.csv s3://bucket1/ twitter-dataCollection/running_results/hate_5000-1-result.csv
```

