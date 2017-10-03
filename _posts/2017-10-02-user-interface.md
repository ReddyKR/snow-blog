---
layout: post
cover: 'assets/images/cover4.jpg'
title: A Beginner’s Insight into the User Interface on ServiceNow
date:   2017-10-02 10:00:00
tags: tips
subclass: 'post tag-test tag-content'
categories: johnlee
navigation: True
author: 'John Lee'
nickname: johnlee
bio: "Certified ServiceNow Application Developer and System Administrator"
image: 'assets/images/jlee.jpg'
logo: 'assets/images/jg_logo_white.png'
---
<p>
  As a new developer, working on the platform for about 5 months, these are some of the thoughts I have on the front-end development for ServiceNow. This post is targeted towards people that have just gone through ServiceNow’s Learning Plan, started getting used to the platform, or just generally curious on how ServiceNow approaches interfaces/design. Veterans are more than welcome to expand on ideas that are going to be listed here and give any helpful insight.
</p>
<p>
For an application that is consumed by an end user, the best practice is to create a separation between front-end design and back-end logic - this is known as the MVC pattern. It keeps projects clean and priorities focused. Within ServiceNow, it’s initially hard to see that division. You can go to the platform’s browser IDE, Studio, and look through your application to see the various sections in the Application Explorer. You have tabs like Forms & UI that lets you customize your forms and how your lists are presented, but they sit next to things like business logic scripts. It’s all encompassing and from the initial pass through, the application feels complete. Eventually it gets added as another module on the list of applications on the main browser.
</p>

<p>
  <img src="assets/images/UserInter/BasicSite.jpg" alt="Test Image" />
</p>

<p>
  …But is it done? It isn’t some sort of JSON being displayed on a command window but it is bare in aesthetics. What if you want a more engaging interface for your users? The list views are practical but ask any front-end developer (or end-user, for that matter) and they’ll immediately ask for alternatives. With over a decade worth of feedback and upgrades, ServiceNow has created other options for developers to make their instances or applications visually appealing. Its interesting to see how much it’s progressed and explore what these options are.
</p>

<hr />

<h3 id="angular4">The Angular2/4 Experiment</h3>

<p>
<a href="http://angularjs.blogspot.com/2017/03/angular-400-now-available.html">Angular 4</a>, formerly Angular 2, is the newest version of the popular AngularJS front-end framework led by the Angular Team at Google. For new projects that are not weighed down by legacy projects or pre-existing requirements, it’s great to use a newer version of a tool. Pair Angular 2/4 up with angular-cli and you have a great system of generating files, testing, and managing front-end development. That said, it’s a shame ServiceNow does not currently support it (Jakarta).  If developers do want to pursue this route, it would most likely be a stand-alone front-end app that would use ServiceNow as their back-end. It would save a lot of headache just waiting for ServiceNow to support it, but it is feasible. Check out Nathan Grove’s Angular 2 set-up and the workshop he led on a sample Angular2 App:
</p>

<p><a href="https://community.servicenow.com/docs/DOC-6626">Angular2 Development Environment</a></p>
<p><a href="https://community.servicenow.com/docs/DOC-6788">Angular2 applications for the ServiceNow platform</a></p>

<p>
  <img src="assets/images/UserInter/Angular4_Attach_Test.gif" alt="Angular4 Test Attachment" />
</p>
<p><small><i>
The application is a little silly, but does illustrate the point he's trying to make. Here, from the REST API Explorer, we can update a record. Navigating to the record, we can see the changes that have been applied.
</i></small></p>

<p>
  <img src="assets/images/UserInter/Angular4_Attach_Application.gif" alt="Angular4 Application Attachment" />
</p>
<p><small><i>
Extending further pass the REST API test, we can actually use Nathan Grove's application to create an image, list all the records of specific table, and even attach the image onto it.
</i></small></p>

<p>
It seems to defeat the purpose of building something outside of ServiceNow and miss out in features built into the platform, but there is merit in having loosely coupled applications. It would be simple enough for you to move from ServiceNow and attach this onto some other framework if you needed to. If we want to stay on the platform, however, we could jump back to what ServiceNow currently supports: AngularJS.
<p>
