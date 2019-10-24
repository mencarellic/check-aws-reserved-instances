# check-aws-reserved-instances

This script shows summary about using "Reserved" and "On-demand" ec2 instances. Namely:

* Which "On-demand" instances haven't got a "Reserved" instance;
* Which "Reserved" instances are unused;
* And which "Reserved" instances are expiring soon.

The script is heavily based on Scott Bigelow's work: https://github.com/epheph/ec2-check-reserved-instances and Timon Wong's work: https://github.com/timonwong/check-aws-reserved-instances

## Requirements

* Python 2.6+
* argparse (required when using Python 2.6)
* boto3

## How to work with it

For the script needs your [AWS Security Credentials](http://docs.aws.amazon.com/AWSSecurityCredentials/1.0/AboutAWSCredentials.html).

You can specify them in [the Boto config](http://boto3.readthedocs.io/en/latest/guide/configuration.html) (`~/.boto` or `/etc/boto.cfg`) or using script command line arguments or by exporting in an environment variables (`AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`).

You can also specify an AWS profile with the `-p` or `--profile-name` flag.

Example:

```
host# export AWS_ACCESS_KEY_ID=ABCDE
host# export AWS_SECRET_ACCESS_KEY=5ji7haengeeFoh8eziebeu
host# ./check-reserved-instances --region us-west-1 -w 60
Unused reserved instances:
    (2)	Linux/UNIX m1.small	us-west-1c
    (3)	Linux/UNIX m1.large	us-west-1c

Soon expiring (less than 60d) reserved instances:
    93bbbca2-d072-4dcc-bb7e-7c137ad565f7	Linux/UNIX m1.small	us-west-1c	2014-04-15
    bbcd9749-4bf0-440a-bf53-3641e3732b73	Linux/UNIX m1.small	us-west-1c	2014-04-03

On-demand instances, which haven't got a reserved instance:
    (1)	Linux/UNIX m3.medium	us-west-1c
    (3)	Linux/UNIX m1.large	us-west-1b
    (1)	Linux/UNIX m1.medium	us-west-1b

Running on-demand instances:   27
Reserved instances:            22
```

For more help use the `-h` flag
