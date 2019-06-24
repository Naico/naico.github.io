---
layout: post
title: Google Tag Manager and Google Analystics
categories: Javascript
description: A brief instruction to GTM and GA
tags: Google-Tag-Manager Google-Analystics
---

Our team are now working on adding google tracking code to track user behavior or other targeted params, to collect user behavior and user preference.

During this working period, we met some strange behavior for the 2 features. We gathered them as question and answer and generated the list here, to help the one who is or will be working on the related feature.

In this article, we will use GTM and GA to abridge the two features.

If you met more strange issues, then please help to contribute to this article.

# What is GTM and GA?
Google Analytics is well known as a famous analyst tool published by google inc. Now the project is expanded to a whole analysis system named as Google Analytics Solution. 

>Google Analytics is a powerful analytics solution for companies of all shape and size.

Google Tag Manager is a new feature under Google Analytics Solution and it is used to combine all kinds of Google Analytics Features.

>Google Tag Manager offers simple, yet powerful tag management solutions to help small businesses and large enterprises launch programs faster.

So we can see that GTM is a container feature, and GA is a application feature which can be 'plugin into' GTM container.

# Why using GTM instead of GA?
In the previous version, if we want to include GA to your solution, we need to insert a certain script section to you website and config the needed parameters.

Meanwhile, if you want to add more 3rd party analytics tools powered by google, you need to add more code section to your solution. This is really wired.

GTM came out to be a successful solution to include all of these kind of features. Once you implemented the GTM to your website solution, you are able to including all the supported features by changing the config in the tag manager website.

Each feature is recognized as a Container, and inside the container, we will have different tags to tracking different types of tracking params.

In a word, GTM is a combined container collection which will be more powerful and less code injection to your website.

# How to implement GTM and GA?

Please refer to the following link for more details:
[Link](https://support.google.com/tagmanager/answer/6102821?hl=en&ref_topic=3441530)

[Link](http://westore.farfetch.cn/home?utm_source=analystics_test&utm_medium=referral&utm_campaigns=FF_PROMO_TEST)

[Link to Alex-Feng](http://www.alex-feng.com/home?utm_source=wechat&utm_medium=affiliate&utm_campaign=PHCN)

[Link to DEV](http://westore-dev.farfetch.net/home?utm_source=ipinyou&utm_medium=display&utm_campaign=CN_WeChatMP_PROS_WeChatStoreX20_Link)

[PH Link Test](http://www.alex-feng.com/home?clickref=1101l4DeH6ir&utm_source=test_george&utm_medium=affiliate&utm_campaign=PHCN&utm_term=CNNetwork&pid=performancehorizon_int&c=test_george&clickid=1101l4DeH6ir&af_siteid=1100l17836&af_sub_siteid=1011l267&af_cost_model=CPA&af_channel=affiliate&is_retargeting=true)
