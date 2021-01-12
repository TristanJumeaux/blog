---
author: "Tristan Jumeaux"
date: 2020-10-29
title: How did I deployed this blog
---

## Introduction

This blog post will explain you quickly how I deployed this website powered by Hugo and hosted by AWS.  <br  />

First of all, I have created this blog as a student. Hence, I am aware that every isn't perfect. 
Feel free to give me any tips or potential improvements.<br  />

This post is composed of an introduction to Hugo and an explanation of the AWS process.  <br  />
The goal is to regroup the resources that helped me building it. You will find many redirection to official tutorials. 
Let's start by exploring Hugo.



## Hugo

### 1.1 Hugo ?

Hugo is one of the most popular open-source static site generators. 
It is very well documented, here are some interesting articles :

* [What is Hugo ?](https://gohugo.io/about/what-is-hugo/)
* [Install Hugo](https://gohugo.io/getting-started/installing/)
* [Quickstart](https://gohugo.io/getting-started/quick-start/)

I advise you to read these different pages and to start installing and playing with Hugo.

### 1.2 Make a choice.

Now that you have installed Hugo, you have to scroll for some minutes through this [page](https://themes.gohugo.io/) that contains plenty of different designs!
Once you found your theme, pull it using git. Things are becoming real!

You can start customizing it and adding (or removing) the content you want.
To do so, I recommend you the following command. 

```
hugo server -w
```

It updates your localhost server everytime you make a change in a local file without the need of restarting the server.
When you are done with your local website, execute the following command.

```
hugo
```

Following this, you will find out that a new folder named "Public" has been created.
This folder contains every files you need in order to run your website.
This is what needs to be upload to your S3.
You can try your website by opening your index.html file.

Now that we have our website ready, it's time to make it available to the world! 

## AWS

#### 2.1 Sign up!

Firstly, if you do not have any AWS account and you want to host your website, start by creating a [free account.](https://aws.amazon.com/fr/free/?trk=ps_a134p000003yhaiAAA&trkCampaign=acq_paid_search_brand&sc_channel=ps&sc_campaign=acquisition_FR&sc_publisher=google&sc_category=core&sc_country=FR&sc_geo=EMEA&sc_outcome=Acquisition&sc_detail=aws%20sign%20up&sc_content=Signup_e&sc_matchtype=e&sc_segment=454820904213&sc_medium=ACQ-P|PS-GO|Brand|Desktop|SU|AWS|Core|FR|EN|Text&s_kwcid=AL!4422!3!454820904213!e!!g!!aws%20sign%20up&ef_id=CjwKCAiA-f78BRBbEiwATKRRBExe_IFxJ-SzjdKPFxabZzQ1mbti4TOwF0rlyA55A8XSrKRSw8P9WhoC7X4QAvD_BwE:G:s&s_kwcid=AL!4422!3!454820904213!e!!g!!aws%20sign%20up&all-free-tier.sort-by=item.additionalFields.SortRank&all-free-tier.sort-order=asc)
After doing so, create an [IAM User](https://docs.aws.amazon.com/fr_fr/IAM/latest/UserGuide/id_users_create.html) and connect to this account instead of your root account.
This is highly recommended for security reasons.

#### 2.2 Store your files.

Now that you are connected in your IAM User account, use the console to open the S3 service.
Create a bucket with the name that would like to give to your website.
As an example you can see thanks to the following image the name of my bucket. 
![s3bucket](https://user-images.githubusercontent.com/35367623/98695707-3a39a680-2373-11eb-8f12-6dffbb6fcce7.PNG)

The next step is to upload your __Public__ folder generated earlier.
Make sure to allow public access to the files.

The part about storage has reached its end ! You have everything necessary in your bucket.
The remaining work consists in the redirection of users to your website!

#### 2.3 Buy a domain name.

If you are new to AWS, it offers a DNS service called Route53.
More, Route53 doesn't limit himself to routing. You can also buy your [domain name](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/domain-register.html) thanks to this service.
I hope that you thought about it. Else, take 5 minutes, it is quite important !

#### 2.4 Creating your highway.

Following this [tutorial](https://aws.amazon.com/fr/premiumsupport/knowledge-center/cloudfront-serve-static-website/) you will be able to create the bridge between your domain name
and your S3 endpoint.

We will take advantage of the CloudFront component which gives us a worlwide distribution and caching service of our website.
This tutorial will also provide your website with a certificate that will make it https complient.

## Congratulations

Congratulations, you've done it ! You should now be able to access your blog via your favourite web navigator.