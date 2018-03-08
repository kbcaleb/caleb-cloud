---
title: Install AWS CLI on OSX
date: 2015-10-06 20:44:52.000000000 -06:00
categories:
  - aws
tags:
  - aws
header:
  teaser: "/assets/images/aws.png"
  show_overlay_excerpt: false
---

You are going to need to make sure you meet a few requirements to install the CLI tools but you should already have most in place.
```shell
Python 2 or Python 3.3+
Pip
```
First verify your python version.
```shell

python --version

```
You should get a response similar to this.
```shell

➜  ~  python --version
Python 2.7.10

```
Now check for Pip support
```shell

pip --help

Usage:
  pip <command></command> [options]

```
If you do not have Pip installed here is a quick HOWTO
```shell

curl -O https://bootstrap.pypa.io/get-pip.py
sudo python get-pip.py

```
Now install the AWScli tools
```shell

pip install awscli

```
NOTE: Currently there is a bug in El Capitan because it already has six-1.4.1 installed and AWS CLI wants to install &gt;=1.5 which causes another whole set of issues with Apple System Integration Protection. Still waiting for responses on the interwebs for a fix from apple.
I would recommend using the bundled version in El Captain until this gets sorted out.
```shell

curl "https://s3.amazonaws.com/aws-cli/awscli-bundle.zip" -o "awscli-bundle.zip"
unzip awscli-bundle.zip
sudo ./awscli-bundle/install -i /usr/local/aws -b /usr/local/bin/aws

```
Now you can verify it is all working with
```shell

aws --version

aws-cli/1.8.11 Python/2.7.10 Darwin/15.0.0

```
Now you will need to configure the CLI to allow for access to your account. You will need your accounts Access Key ID and Secret Access Key.
```shell

aws configure --profile yourprofilename
AWS Access Key ID [None]: YOURKEYGOESHERE
AWS Secret Access Key [None]: yoursecretkeygoeshere
Default region name [None]: us-east-1
Default output format [None]: json

```
On mac this will create the following file for reference.
```shell

/Users/username/.aws/credentials

```
Now verify you can pull data on your account.
```shell

aws ec2 describe-instances --profile yourprofilename

```
You can change many of your call on the CLI as far as --profile --output and --regions.
```shell

aws ec2 describe-instances --profile yourprofilename --output table --region us-west-2

```
