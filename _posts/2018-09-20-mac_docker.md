---
layout: post
title: "Mac update to 10.+ using brew cannot write to /usr/local"
description: "Mac升级10.1.3后出现了brew 下载第三方包,不能写入/usr/local的问题"
categories: [Tools]
tags: [brew]
redirect_from:
  - /2018/09/20/
---

Using brew to download a package on Mac may occur the problem that could not write to /usr/local.

Since brew could not support run by root, and normal user could not write to /usr/local.  Therefore, we need to modify the authority for /usr/local

However, since Mac enables the Rootless mechanism to protect the core, enter:
'''
csrutil status
'''

on terminal, and it shows:
{% highlight ruby %}
System Integrity Protection status: enabled.
{% endhighlight %}

which means the Rootless protection in enabled on your Mac.

There are several ways to solve the problem

**1.Force to update brew**
'''
 /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"; 
'''

**2. close Rootless**
Restart your mac and press *command+R* at the same time to enter the recover mode.
Find the terminal in the menu and enter 
'''
csrutil disable
'''

and restart your computer, then you could find that:
{% highlight ruby %}
System Integrity Protection status: enabled.
{% endhighlight %}

now your could use *sudo* to change the authority.

**!!Using ''' csrutil enable''' to change It Back After Finished!!**

**3. Just go to the official website to download...**
