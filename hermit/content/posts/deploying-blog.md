---
author: "Tristan Jumeaux"
date: 2020-10-29
title: How did I deployed this blog
---

## Introduction

This blog post will explain you quickly how I deployed this website.
It is powered by Hugo and AWS.


## Steps

1. Hugo

1.1 Hugo ?

Hugo is one of the most popular open-source static site generators. 
It is very well documented, here are some interesting articles :

* [What is Hugo ?](https://gohugo.io/about/what-is-hugo/)
* [Install Hugo](https://gohugo.io/getting-started/installing/)
* [Quickstart](https://gohugo.io/getting-started/quick-start/)
;
I advise you to read these different pages and to start installing and playing with Hugo.

1.2 Make a choice

Now that you have installed Hugo, you have to scroll for some minutes through this [page](https://themes.gohugo.io/) that contains plenty of different designs!
Once you found your theme, pull it using git. Things are becoming real!

You can start customizing it and adding the content you want.
To do so, I recommend you the following command. 

It updates your localhost server everytime you make a change in a local file.

'''
hugo server -w
'''

When you are done with your local website, execute the following command.

'''
hugo
'''

Following this, you will find out that a new folder named "Public" has been created.
This folder contains every files you need in order to run your website.
This is what you will upload to your S3.

2. AWS

2.1 Create an AWS account. Create IAM user, disconnect from your account and always connect to your IAM user.
2.2 Create an S3 bucket and upload your public folder to your S3.
2.3 Customize the bucket policy and CORS to make it work.
2.4 Buy a domain name.
2.5 Create a cloudfront distribution that will link your domain name with your S3 endpoint using an SSL certificate.

Congratulations, you've done it !