---
title: AWS EC2 Instruction
date: 2021-07-01
permalink: /posts/2020/10-AWS-setting
excerpt_separator: <!--more-->
toc: true
tags:
  - regex
---

**Step 0: Install PuTTY in windows**

PuTTY is a free implementation of SSH for Windows. You can download the PuTTY installer from the following link: [https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)

![](RackMultipart20211222-4-n35wz9_html_43514da88adaeb51.png)

Choose the version you need for your windows system accordingly.

**Step 1: Login in Amazon AWS and launch an EC2 instance.**

After you login your account, open the services and go to EC2 dashboard.

<!--more-->

![](RackMultipart20211222-4-n35wz9_html_1cca940e01c3d453.png)

Click &quot;Launch instance&quot; under the drawer of &quot;Launch instance&quot;.

![](RackMultipart20211222-4-n35wz9_html_dab8e1884d789eb5.png)

Select &quot;**Amazon Linux AMI 2018.03.0 (HVM), SSD Volume Type** - ami-027cab9a7bf0155df&quot; as Amazon Machine Image (AMI).

![](RackMultipart20211222-4-n35wz9_html_529b52294faadabd.png)

Select &quot;r5d.large&quot; as your instance type and then click &quot;Next: Configure Instance Details&quot;.

![](RackMultipart20211222-4-n35wz9_html_4e69354b6bd147eb.png)

Don&#39;t change any setting and click &quot;Next: Add storage&quot;.

![](RackMultipart20211222-4-n35wz9_html_ce11983961896fad.png)

Click &quot;Next: Add Tags

![](RackMultipart20211222-4-n35wz9_html_4fe52bc23cb2cefe.png)

dg

![](RackMultipart20211222-4-n35wz9_html_49a915ea4c7ec7d5.png)

Move to next page and click &quot;Launch&quot;. Choose &quot;Create a new key pair&quot; and give a key pair name in the pop-up window.

![](RackMultipart20211222-4-n35wz9_html_2368bc07a98fd5d4.png)

And then click &quot;Download Key Pair&quot;. Please keep your key pair in a safe place. It will be used to connect to EC2 from the local machine. After you download the file, click &quot; Launch Instances&quot;.

![](RackMultipart20211222-4-n35wz9_html_1868adbc2a132907.png)

Now you have launched EC2 instance.

**Step 2: Convert public key to private key**

Open PuTTY Key Generator and click &quot;Load&quot; to locate the key pair file you download. And then click &quot;Save private key&quot;.

![](RackMultipart20211222-4-n35wz9_html_17a16c48acb1e4f.png)

**Step 3: Connect to EC2 from local**

Go to EC2 dashboard and check running instances. Copy &quot;Public IPv4 DNS&quot;.

![](RackMultipart20211222-4-n35wz9_html_b45e4661b36b19df.png)

Open PuTTY. At blank of host name, type &quot;ec2-user@&quot; and paste the address you just get.

![](RackMultipart20211222-4-n35wz9_html_e65b37e0694a0797.png)

In the **Category** pane, choose **Connection** , **SSH** and **Auth**. Complete the following:

- Choose **Browse** , select the .ppk file that you generated for your key pair, and then choose **Open**.
- Choose **Open** to start the PuTTY session.

![](RackMultipart20211222-4-n35wz9_html_ae1cf06c9a63abcb.png)

So now you can connect to EC2 instance from local.

![](RackMultipart20211222-4-n35wz9_html_f9f37f2a6f94c216.png)

**Step 4 AWS configuration**

Run this command to quickly set and view your credential, region and output format. The following example show sample values.

![](RackMultipart20211222-4-n35wz9_html_b647bfa17b5e3558.png)

Replace AWS access key id and AWS secret access key to your own ones.

**Step 5 Install Python 3, pip 3, and the EB CLI on instance**

In Linux command line, type as shown in the figure.

![](RackMultipart20211222-4-n35wz9_html_3534bfbbf341823b.png)

Type &quot;y&quot; and click enter.

![](RackMultipart20211222-4-n35wz9_html_e9978132e6405dcc.png)

Install pip for python 3. Download the installation script.

![](RackMultipart20211222-4-n35wz9_html_6e75432bd8b70a8b.png)

$ curl -O https://bootstrap.pypa.io/get-pip.py

Run the script with Python.

![](RackMultipart20211222-4-n35wz9_html_66b751f986f11f6d.png)

Use pip to install the EV CLI

![](RackMultipart20211222-4-n35wz9_html_d55adcbcf58bf64e.png)

**Step 6 Install Python packages for the project**

![](RackMultipart20211222-4-n35wz9_html_232a8b38c317fa5a.png)

![](RackMultipart20211222-4-n35wz9_html_894d9464b8086597.png)

**Step 7 Load data and python program into EC2 instance**

Use the following command to copy an object from Amazon S3 to your instance.

[ec2-user ~]$ aws s3 cp s3://my\_bucket/my\_folder/my\_file.ext my\_copied\_file.ext

Eg:

![](RackMultipart20211222-4-n35wz9_html_8dc0abfca8d6d947.png)

Use the same method to load python program &quot;Tweets\_scraper.py&quot; into EC2 instance.

Make sure both data and python program are in instance already using the command below.

![](RackMultipart20211222-4-n35wz9_html_d9efbe219852a76d.png)

**Step 8 change data file name and output file name in the python code and add your Twitter API token into the code.**

![](RackMultipart20211222-4-n35wz9_html_e2ff9d998f06493f.png)

Change the load file name to the one you copy to EC2 instance. Add your consumer key, consumer secret, access token and access token secret into the code.

This link is for how to get API Keys and Tokens for Twitter: [https://www.slickremix.com/docs/how-to-get-api-keys-and-tokens-for-twitter/](https://www.slickremix.com/docs/how-to-get-api-keys-and-tokens-for-twitter/)

![](RackMultipart20211222-4-n35wz9_html_ef6066f55641214a.png)

Change the output file name accordingly. If &#39; **hate\_5000-1.csv**&quot; is your input file, your output file name should be &quot; **hate\_5000-1-result.csv**&quot;. Use PgDn to move to the bottom of the code.

![](RackMultipart20211222-4-n35wz9_html_93b2cdfee922d322.png)

After these, press Ctrl+X, y and Enter in order.

![](RackMultipart20211222-4-n35wz9_html_7904e57e9f2359d3.png)

**Step 9 Run the python program**

![](RackMultipart20211222-4-n35wz9_html_e4e4762750f9823c.png)

**Step 10 Save your output file into S3 storage.**

Use the command to save file into S3 storage. Please put into running\_results folder.

**[ec2-user@~] $ aws s3 cp hate\_5000-1-result.csv s3://ircovid19project/ twitter-dataCollection/running\_results/hate\_5000-1-result.csv**
