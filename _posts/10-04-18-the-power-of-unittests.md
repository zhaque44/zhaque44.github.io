---
layout: post
title: The power and flexibility of unittest paired with requests…
date: 2018-04-10 04:00:00
tags: unittesting flexibility requests
author: Zubair Haque
---
In my current role I am the only Software Development Engineer in Test in charge of all Quality Control Processes and activities in a fast paced <i><b>Continuous Integration</b></i> model. The team that I am a part of is working on modernizing a product platform that is currently deployed in several countries worldwide. The APIs have documentation which describes what endpoints require what <i><b>headers and parameters</b></i>, as well as what different <i><b>response status codes</b></i> to expect and so on. Being short-staffed, I needed to pick a framework that would be <i><b>lightweight</b></i> & <i><b>easy to pick up</b></i>. Also, it should be something the <i><b>entire</b></i> team is comfortable with (I <i><b>stress</b><i/> that the most, because of the following):

<code>When your team is continuously making changes and you have coverage with a good set of tests, your team members will rely on the testing suite prior to merging changes. </code>
