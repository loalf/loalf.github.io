---
layout: post
title:  "Managing multiple SSH accounts in Github"
comments: true
date:   2016-03-02 09:46:52
categories: github ssh
---

<p>
Lots of companies are using Github nowadays for hosting their private repositories.
If you are like me and you don't like mixing up your public/private personas, you
might want to have a couple of Github accounts, one for business and one for your
personal matters.
</p>

<p>
Let's see how to achieve this.
</p>

<h2>Create your SSH keys</h2>
In this case, I'll be creating two SSH keys, one for <code>loalf</code> (my public profile)
and another one for <code>humandb</code> (the corporate one).

{% highlight shell %}
$ ssh-keygen -t rsa -b 4096 -C "personal_email@youremail.com"
$ ssh-keygen -t rsa -b 4096 -C "company_email@youremail.com"
{% endhighlight %}

Two keys will be created

{% highlight shell %}
~/.ssh/id_rsa_humandb
~/.ssh/id_rsa_loalf
{% endhighlight %}

<h2>Modify your SSH config file</h2>
Next, you'll have to edit your SSH config file. You config file should be at <code>
~/.ssh/config</code>. If it doesn't exist, just create it.

{% highlight ini %}
Host loalf.github.com
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_rsa_loalf

Host humandb.github.com
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_rsa_humandb
{% endhighlight %}

<h2>Clone your repository</h2>
If you want to clone one of your repositories as <code>loalf</code> you now do

{% highlight shell %}
git clone git@loalf.github.com:loalf/your-repo.git
{% endhighlight %}

Note that instead of using <code>github.com</code> as the host, we're using
<code>loalf.github.com</code> instead.

<h2>Set up your username and email address</h2>
Change your git username and email address within the project.

{% highlight shell %}
$ git config user.name "loalf"
$ git config user.email "f12loalf@gmail.com"
{% endhighlight %}
