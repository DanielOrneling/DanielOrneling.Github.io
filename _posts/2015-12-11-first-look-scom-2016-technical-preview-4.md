---
title: "A first look at SCOM 2016 Technical Preview 4"
date: "2015-12-11"
excerpt_separator: "<!--More-->"
categories: 
  - "operations-management-suite"
  - "operations-manager"
  - "orneling-se"
---

And so that beautiful time has come again (I admit I´m a little late with this one as its been out for about three weeks now) when a new technical preview has been released of System Center 2016. This time, the term Technical Preview is followed by the number 4. In my last "technical preview post", I went through the news of number 2. If you want to read that post, you will find it [here](http://blog.orneling.se/2015/05/a-first-look-at-the-scom-2016-technical-preview-2/){:target="_blank"}.
<!--More-->
**So what´s new this time?**

I have chosen not to show the installation process since there is no difference from the earlier preview other than it´s now installable on the Technical Preview 4 of Windows Server 2016. The first thing you will notice when launching the installation or the Operations Console is that it now says System Center 2016 instead of 2012.

![](https://blog.orneling.se/assets/images/2015/12/121115_0936_Afirstlooka1.png)  Once you´ve opened the console, you will find some slight differences in the Administration pane. You now have two "Management Packs" sub menus, Installed Management Packs which shows all MP´s just like before, but you will also see the new "Updates and Recommendations" section. This section will show you those MP´s that should be imported based on what roles and functions your servers fill.

![](https://blog.orneling.se/assets/images/2015/12/121115_0936_Afirstlooka2.png)

The picture below was taken just after I installed SCOM 2016 TP4 and as you can see, it recommends me to import the IIS MP just like the Core OS MP for Windows Server 2016. This is based on a first scan of my servers and the agent reports back to SCOM what is actually installed on it. You will be given the opportunity to get a single MP to fill a single recommendation or to "Get all MP´s" to fulfill all recommendations. The MP´s will then be downloaded via the management pack catalog.

![](https://blog.orneling.se/assets/images/2015/12/121115_0936_Afirstlooka3.png)

The next thing that is new (for SCOM 2016) is the Maintenance Schedules. This was present in the TP2 as well but I will go through it again below, just because this is a very welcome feature in this 2016 version of SCOM. A more detailed deep dive is to be found in my TP2 post which I linked to in the beginning of this post.

![](https://blog.orneling.se/assets/images/2015/12/121115_0936_Afirstlooka4.png)

The first thing to do is to point out either a single object or a custom group that should be affected by the maintenance window.

![](https://blog.orneling.se/assets/images/2015/12/121115_0936_Afirstlooka5.png)

The maintenance schedule is the next thing. In this case I will have a monthly patch window the second Wednesday of the month from 22.00-02.00 (10pm to 2am).

![](https://blog.orneling.se/assets/images/2015/12/121115_0936_Afirstlooka6.png)

Finish by naming the maintenance schedule and give it a category. The maintenance mode categories are those you´re used to since earlier SCOM versions so there´s no news in this part. Type a comment as well if you´d like and then your good to go.

![](https://blog.orneling.se/assets/images/2015/12/121115_0936_Afirstlooka7.png)

Below you will see a summary of your schedules, the last time they ran, the next run time and if they´re enabled or disabled.

![](https://blog.orneling.se/assets/images/2015/12/121115_0936_Afirstlooka8.png)

One of the last thing I want to show is the new version number, 7.2.10583.0. In SCOM 2012 R2 the version number was 7.1.10226.0. If you ever run into a wall where you need to check version and build numbers, I strongly recommend [this link](https://buildnumbers.wordpress.com/scom/){:target="_blank"}.

![](https://blog.orneling.se/assets/images/2015/12/121115_0936_Afirstlooka9.png)

**Summary**

The new features that I´ve shown in this post is what I´ve been able to find so far without a real deep dive into databases etc. Based on what I´ve found so far during the preview of SCOM 2016, I think we have some really great new features to look forward to and when we connect it to Operations Management Suite (OMS) as well, we really extend our SCOM environment to give us a lot of additional possibilities.

Have you tried out any of the technical previews of SCOM 2016 so far? If you have, what do you think of it so far? Leave a comment below if you have any input or questions on the post and I´ll get back asap.
