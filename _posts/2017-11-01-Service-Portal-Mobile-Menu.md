---
layout: post
cover: 'assets/images/cover3.jpg'
title: Fix Mobile Menu on Service Portal
date:   2017-10-04 10:18:00
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

While developing an application for Service Portal you are given many features out of the box. You get an responsive environment with widgets that you can use on several pages. But what if you need to change some of that out of the box parts? After having my application tested I was given a task to change the behaviour of the menu on mobile view.

## How it works now
![Incorrect](/assets/images/MenuMobile/mobile-menu-incorrect.gif)
During the testing the mobile menu was inconsistent. When pressed on one of the options it sometimes did collapse, the other times it did not.

## How it should be
![Correct](/assets/images/MenuMobile/mobile-menu-correct.gif)
I was asked to change the menu to collapse every time you click a link. Overall, you usually want to see the page after clicking the menu link, and not have to collapse it every time manually. It would be nice if you could choose if you want it to collapse or not in the Service Portal Menu configuration, but there is none. Then again, the current behaviour makes it collapse once every few times, which is unacceptable.

##  Changing it

Fortunately, there is an easy fix to that. All you need to do is go to Service Portal Menu application:

![Menu](/assets/images/MenuMobile/service-portal-menu.jpeg)
Select the Header Menu that your Service Portal use.

There are options for changing Menu as a widget itself. You can modify it to your need, but the change that we need to make is not in this widget itself, but in an angular template. Therefore you need to scroll down, select *ng-template* tab and click on *menuTemplate*:

![menuTemplate](/assets/images/MenuMobile/menu-bottom.jpeg)

At this point you may need to change the current application scope to global, or just use the link that is on the popup showing if you are in a different scope than global. After that you can change the code:

![Code change](/assets/images/MenuMobile/menu-template.jpeg)

All the changes we need to do is going to happen in the first line. You should add *data-toggle* and *data-target* to the anchor tag:
``` html
<a data-toggle="collapse" data-target=".navbar-collapse" ng-if="item.items.length == 0 && !item.scriptedItems" ng-href="{{item.href}}"  title="{{item.hint}}">
```
Keep in mind that if you had any *toggle* or *target* parameters inside an element, you need to get rid of them.

You are done! Now you need to save this changes by clicking *Update* in the top right corner and test the changes.

##  Summary

There are few things you need to keep in mind when doing this change. First of all, this is appicable to all the applications using this Header Menu widget on the instance. Then, if you want the change to apply to you application, you need to redo all this steps on every instance (because you are modifying original header). If you need to have the change bind with your application if should work if you clone this header and use it as your own custom widget. Lastly, this is a change to existing code, that was created by ServiceNow itself, tested and deployed to be used by the customers. My change may break something, that I am not able to check. Therefore after doing this change, test your application and check if it meets your requirements, because I am not responsible for anything that will happen after following this tutorial.