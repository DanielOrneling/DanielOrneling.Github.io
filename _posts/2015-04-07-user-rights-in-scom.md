---
title: "User rights in SCOM"
date: "2015-04-07"
excerpt_separator: "<!--More-->"
categories: 
  - "operations-manager"
  - "orneling-se"
---

One thing that I often come across in my projects of implementing SCOM at customers is the ability to assign user rights in SCOM to specific users or groups. As an Operations Manager admin, you have access to all there is and you can completely mess up (or worse) the environment. Do we really want everyone to be an Operations Manager admin with this knowledge? If the answer to that question is yes, think it over a couple more times J. If the answer is no (hopefully it is), then keep reading to find out how it´s done.
<!--More-->
**Logging on as an administrator**

Below, I´m logging into SCOM (from outside the domain) with a user that has administrative rights.

![](https://blog.orneling.se/assets/images/2015/04/040215_0835_Userrightsi1.png)

As you can see here I have complete access to all that is monitored meaning I can see all that´s being monitored, install new agents etc. This also includes all tasks for setting a database offline, running defrag on a disk and so on. This is where we want to limit our users to only see what their interested in and match what they see with their role. For example, a person working as a SQL administrator don´t need information about the monitoring of AD FS, IIS or Windows Server Remote Access etc.

![](https://blog.orneling.se/assets/images/2015/04/040215_0835_Userrightsi2.png)

To create a new user role, navigate to Settings and then User Roles as seen below.

![](https://blog.orneling.se/assets/images/2015/04/040215_0835_Userrightsi3.png)

Choose which role you´d like (read more about the different roles at [TechNet](https://technet.microsoft.com/en-us/library/hh872885.aspx)).

![](https://blog.orneling.se/assets/images/2015/04/040215_0835_Userrightsi4.png)

Set a name for the role, in this case IIS Admin and then pick the user(s) which should be included in the role. You can also choose an AD group instead of the specific users. By using groups, you don´t need to go into SCOM every time you want to add a user to the role when it can be done in the AD instead.

This Operator role has the following opportunities;

_"The Operator profile includes a set of privileges designed for users that need access to Alerts, Views and Tasks. A role based on the Operators profile grants members the ability to interact with Alerts, execute Tasks and access Views according to their configured scope."_

![](https://blog.orneling.se/assets/images/2015/04/040215_0835_Userrightsi5.png)

This is where you choose what the role users should be able to see. Default is everything but instead I´ve checked the IIS parts as seen below.

![](https://blog.orneling.se/assets/images/2015/04/040215_0835_Userrightsi6.png)

Instead of allowing all tasks you can check the ones you´d want them to use. Make a search for Internet Information Services and you´ll see all appropriate tasks.

![](https://blog.orneling.se/assets/images/2015/04/040215_0835_Userrightsi7.png)

![](https://blog.orneling.se/assets/images/2015/04/040215_0835_Userrightsi8.png)

![](https://blog.orneling.se/assets/images/2015/04/040215_0835_Userrightsi9.png)

Now that we´ve created the IIS user role, it´s time to do the same for the SQL admins. This time I´m going to use the Advanced Operator role instead with these rights;

_"The Advanced Operator profile includes a set of privileges designed for users that need access to limited tweaking of monitoring configuration in addition to the Operators privileges. A role based on the Advanced Operators profile grants members the ability to override the configuration of rules and monitors for specific targets or groups of targets within the configured scope."_

![](https://blog.orneling.se/assets/images/2015/04/040215_0835_Userrightsi10.png)

Picking the SQL parts instead followed by the same process for the tasks.

![](https://blog.orneling.se/assets/images/2015/04/040215_0835_Userrightsi11.png)

![](https://blog.orneling.se/assets/images/2015/04/040215_0835_Userrightsi12.png)

![](https://blog.orneling.se/assets/images/2015/04/040215_0835_Userrightsi13.png)

**Trying out the new user roles**

Now it´s time to check out how it looks. The first user I choose is John Doe who is an IIS Admin in the Orneling business.

![](https://blog.orneling.se/assets/images/2015/04/040215_0835_Userrightsi14.png)

As you can see below, only the IIS components is visible. This makes life a lot easier for our friend John who doesn´t get information on all the SQL alerts etc. This way he can focus on his responsibilities and leave the rest of the problems to the other teams.

![](https://blog.orneling.se/assets/images/2015/04/040215_0835_Userrightsi15.png)

Here you can see what tasks are available to John, all of them are IIS related just as it´s supposed to.

![](https://blog.orneling.se/assets/images/2015/04/040215_0835_Userrightsi16.png)

The second user I choose for the SQL admin role is Jane Doe. Jane is a SQL administrator in the Orneling business and she really doesn't care for IIS, AD FS etc. so that´s why I wanted to make life a little bit easier for her.

![](https://blog.orneling.se/assets/images/2015/04/040215_0835_Userrightsi17.png)

As you can see below, only SQL related views are available to Jane so that she can concentrate on the things she´s interested in. What´s different here is that Jane also has the Authoring pane in the console meaning she can create rules, monitors, tasks etc. That´s something she´s allowed to since she´s an advanced operator instead of John´s Operator role.

![](https://blog.orneling.se/assets/images/2015/04/040215_0835_Userrightsi18.png)

And as expected, only the SQL related tasks is visible to Jane.

![](https://blog.orneling.se/assets/images/2015/04/040215_0835_Userrightsi19.png)

**Summary**

As I´ve shown here, it´s really easy to limit your team members access so that they only see what they should focus on. This is as I mentioned something that a lot of my customers are looking at. For you as an administrator to sleep better at night, shouldn't you consider looking into the user role assignment instead of having everyone as an administrator? By the way, if you haven't checked the Administrator role inside SCOM you should probably do it. By default, the local admins on the management server is an administrator and this is one of the first things I edit when SCOM is installed.

Have any questions on this post and how to do it? Leave a comment below.
