---
title: Friendly Git Terminal
description: Friendly Git Terminal
header: Friendly Git Terminal
---
I'm fairly new to using Git.  I started using it in late 2013.  When I first used it, I found it to be a bit overwhelming but after consistently using it, I have found it to be a great tool for source control.  On initial use in the terminal I was always asking myself "What branch am I on?" or "What directory am I looking at?" When looking at ```git log``` I would often say "It would be nice if this was easier to read."  One of the things that has helped me be more proficient with Git, is making the terminal friendlier.

### Improving the terminal prompt by adding the time, user, hostname, current directory, and branch

- **Time**: I like displaying the time because this gives a rough estimate of when the last command was run and finished.  Granted if you open the terminal and don't run any commands the start time will be off but in general for most cases it can be used as a good estimate.
- **User**: This is the current user
- **Hostname**: This is the hostname of the computer
- **Current Directory**: When working in repositories you may have to work in the sub directories this is helpful in knowing where you are. 
- **Branch**: You can be working on multiple branches this will quickly allow you to see the branch you are working on. 

To accomplish the above add the following to your ~./bash_profile

{% highlight shell %}

parse_git_branch() {
  git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'
}
export PS1="[\t] \u@\h \[\033[32m\]\W\$(parse_git_branch)\[\033[00m\] $ "
{% endhighlight %}

In the prompt you will now see something similar to the below.  
{% highlight shell %}
[07:00:00] user@host folder (master) $
{% endhighlight %}
 If you would like to display more information you can look at some additional [Prompt Statement variables](https://ss64.com/bash/syntax-prompt.html)
<br />
### Making the ```git log``` more concise  

Often times you will want to look at the history of commits that you ahve made.  This is done by using ```git log``` however it can be very verbose and take up a lot of real estate.  

{% highlight shell %}
commit d27075822f21219da54a293eb5d3518417a5f421
Author: Roderick Rodriguez
Date:   Sat Feb 25 03:53:35 2017 -0500

    Commit Comment 1

commit e322902583e486605ba2cc9789b3e62ed7010731
Author: Roderick Rodriguez
Date:   Sat Feb 25 03:53:03 2017 -0500

    Commit Comment 2 

commit 0a3d5abceed3b760a0ea582a5d4df65f1d120473
Author: Roderick Rodriguez
Date:   Sat Feb 11 13:09:39 2017 -0500

    Commit Comment 3
{% endhighlight %}


To make the log less verbose but give you enough detail to let you know what is going on, you can create an alias like ```git hist```.  This alias will display each log in one line and only display the date of commit, commit id, comment, and commiter.

To accomplish the above run the following:
{% highlight shell %}
git config --global alias.hist "log -15 --pretty=format:'[%ad] [%h] %s%d [%an]' --date=short"
{% endhighlight %}

Now when typing ```git hist``` you will see something similar to below.  

{% highlight shell %}
[2017-02-25] [d270758] Commit Comment 1 [Roderick Rodriguez]
[2017-02-19] [e322902] Commit Comment 2 [Roderick Rodriguez]
[2017-02-11] [0a3d5ab] Commit Comment 3 [Roderick Rodriguez]
{% endhighlight %}

Here are some other [common aliases](https://githowto.com/aliases) that you may want to add.

For additional Git tips I have found [19 Tips For Everyday Git Use](https://www.alexkras.com/19-git-tips-for-everyday-use/) to be a helpful quick reference.
