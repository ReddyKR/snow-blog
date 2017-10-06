---
layout: post
cover: 'assets/images/cover3.jpg'
title: The Good, the Bad, and the Ugly About ServiceNow from a Developer's Perspective
date:   2014-09-27 10:18:00
tags: platform
subclass: 'post tag-test tag-content'
categories: jakubsynowiec
navigation: True
author: 'Jakub Synowiec'
nickname: jakubsynowiec
bio: "Certified ServiceNow Application Developer"
image: 'assets/images/jsynowiec.jpg'
logo: 'assets/images/jg_logo_white.png'
---

ServiceNow is a big thing now. Over the years platform has been growing and become one of the main topics regarding IT Service Management. Sure, the [list](https://www.servicenow.com/customers.html#all-customers) of companies using ServiceNow is impressive, but it does not show how many people actually use the platform. What really brought it to my attention is that when I mention ServiceNow while talking to people working in big companies, they usually have heard about it and they either know it is being used at company they, or someone else they know work at. With the growing popularity of the platform comes the need for developers. I familiarized myself with the platform, and I built a demo application. This journey taught me various quirks about the platform which I want to share with all the other Developers.

## Developing for the platform
### Long way until coding
First thing that I have noticed when developing the application is that there is a long way until you will actually start coding. This is very weird comparing to what I am used to. Naturally, I am skipping the step of defining requirements and creating ERD diagrams because it is no different than the process for creating any other app, and talking about building the actual app. In ServiceNow usually one of the first things you want to is create database tables. And you do that through ServiceNow Studio, which is a web-based IDE, using graphical interface - forms, fields and lists - and you can't find any SQL here!

![Studio](/assets/images/studio.png)

The use of graphical based elements while creating the application does not stop there. Many of the pages for you application are semi-done for you. Out of the box you get list views, which allow you to view database data in table-like format. You want to view a specific entry in the table? In ServiceNow it's called a record, and you can view it using Form View. You don't like the layout of the form? There is even a form designer allowing you to drag and drop element to customize that!

So far so good, you don't have to play around with such boring tasks like creating a table view of your data. But your application does not do anything useful yet. You want to have a flow in the app, you want something to trigger actions. You look up how to do that, since you still have not seen any place for writing any code, and you find out that you should do that using workflows. How to create a workflow? There is a workflow editor for that - a drag and drop application that enables you to create and customize workflows.

I hope at this point you can already see my point. An enormous part of the application is being created using ServiceNow specific GUI applications. You may think that this is a great thing! You don't need to learn another API! You do not need to go through setting up annoying things like database connection, user authorization and authentication, basic table and form views. Some of you may also think that this way of doing stuff is completely absurd! How can I work without my beloved IDE, frameworks and libraries? How can I debug and test my code? You have to know that in ServiceNow things are done in a **different** way.
### Implementing Code
Reading this post you may think that you do not need to know how to write code to be able to write an application for ServiceNow. That is wrong. There are places that require coding: business rules, client scripts, script includes just to name few. And if you want to go a step further and write an application with a custom user interface using Service Portal, you need to write JavaScript, HTML and CSS for widgets.

Here is where I encountered my first actual problem with ServiceNow platform. I was very sceptical about having to build the application using provided interfaces from the beginning, but since it was working well, I am able to justify it for the comfort of having all the nice functionality out of the box. But I can find no particular reason to make developers write code inside textareas on the ServiceNow page. I am aware that this way you could write code using, for instance, a chromebook, but that is a step back! Why would you cut your grass using a scythe, when there are lawnmowers created for that?

 Let me show this problem using the widget editor on Service Portal Designer.

![widget](/assets/images/widget.png)

You are greeted by a website where you can edit code in four areas: HTML, CSS, Client Script and Server Script. You start coding, close the JavaScript windows since you want to start with the layout of your widget. You want to resize the CSS area, because usually CSS files aren't very wide, and you want more horizontal space on the HTML template? Sorry. Can't do it. Using your IDE shortcuts? No way of setting them here. Code reformatting? Advanced autocompletion? Jumping around to function definition? No, you are left out without all the things that you like your IDE for.

To give credit, I think ServiceNow is trying to do very well. They provide syntax highlighting, line numbering with the ability to shrink code, a few of the key shortcuts. My point is that no matter how much ServiceNow tries, their IDE is not going to be better than the big guys: Visual Studio, JetBrains or even vim if you are used to that!

### Access to Databases
Another feature that SerivceNow provides to you is a specific way of accessing database. We already know you do not write SQL code to create tables, but what if you want to access them from you JavaScript code? You are left with GlideRecord API. Don't get me wrong - not having to work with SQL is a huge advantage for some, but I would like to make you think for a while. Why does SQL even exist if we could be replacing it with APIs like GlideRecord? The answer is you can't replace it.

On that note so far I am not missing having to write SQL queries. Using the provided API was sufficient enough for me that I did not have any problem with it! I just wanted to add this paragraph because talking to other developers, they were not sure that accessing databases without SQL is a very good design. Again, another thing that ServiceNow does in a **different** way.

### Version Control
Just like every other good developer I follow good practices when it comes to version control. Therefore I have set up a github repository for my ServiceNow application. ServiceNow allows you to do that through Studio. But then I realised some major flaws with this implementation. First of all, I wanted to merge the change that I was developing on my feature branch to master, and realized there is no merge functionality. **What?** Can I revert a commit? That is possible, but not through the Studio. In studio you can apply remote changes, so for reverting a commit you would have to ensure that the commit you want is the most receont one on your branch. Can I look into a previous version of my code? I prefer saying that I am able to instead of I can. Again, you would have to revert to the commit you want to see on your remote repository, apply remote changes and look for the code in the ServiceNow application. At this point I think it is easier to go to your repository, github in my case, and view the XML-enclosed files that define all the code you write inside the application from a revision that you want.

I settled on a workflow that I have found on some ServiceNow [forum](https://snstud.io/using-git-servicenow/), saying that to merge branches you should stash often, then switch branch and unstash. I have not been able to find any official feedback on using git integration for actual version control. Instead, ServiceNow recommends using it for managing versions of the application and easy installing application on developer instances. That means people want to use git as a version control system, but they experience similar problems as I do. Accepting the fact that I have to do the weirdest workaround with VCS system I have ever seen, I was happy to say that it worked for me.

For a few days.

One day, after stashing some changes and trying to unstash them on a different branch, unstashing failed. Up to this day I do not know why did it fail. It said that I have unresoled conflicts in files, and then gave me an empty list of files that I should resolve confilts in. I was annoyed not only because of it not working properly, but because of me losing some work that I have been doing over some time.

## Summary


After reading this post you may think that I absolutely hate ServiceNow platform. That is completly false. I was presented to this platform as something that solves a lot of problems, a great tool that helps IT companies manage the process of producing software, platform that is easily extensible and able to adapt to requirements. Being a very sceptic person I knew there is a catch, nothing is perfect. That is why I wanted to share with everyone out there that is new to this platform as a developer some problems that I have encounter during the beginning of my journey with ServiceNow. I know I did not talk much about the good things, but I think there is enough people saying nice things about it that you could just read their posts.

To give ServiceNow credit I see that there are many changes going in the right direction. Over my relativly short time spent with the platform I have seen an improvement in learning plans that are supposed to help you familiarize with how things work in ServiceNow. I have seen ServiceNow developers implement features that the community requires. I also think that ServiceNow would benefit from allowing people to write their own plugins for ServiceNow that would add functionality they need. There is huge power in community collaboration over certain things. On that note, I started writing my own toolkit that would fix some of my problems listed in this article. Stay tuned for my next post, because when I finish working on the toolkit I will certanly release it for the community.