---
layout: post
title: "Week of the Year"
category: software engineering
tags: [productivity, org-mode]
---

# Week of the Year

For some time, I've been trying to build the habit of tracking things I do and how long it takes me to do them.

The best tool I've found for doing this has been Emacs (Spacemacs) org-mode. The more significant driver towards using it is that it doesn't have a proprietary format. It's all plain text.

One thing that I do consistently is organizing my todo's and notes every week. They look something like this:

![week template example](/assets/images/week_template.png)

The problem is that there's a lot type every week, which reduces the chances of creating a habit.

To solve this problem, I use three tools: Yas-snippets, bash, and Alfred 4.

The format is

```
* --------- Week ## ---------   
  #+BEGIN: clocktable :scope subtree :maxlevel 6 :block 2020-W## :step week
  #+END:

* TASKS
* NOTES
```

First, let's figure out how to get the week number. For that we have bash:

```
> date +%V
32
```

Now we need a way to get that number quickly. That's where Alfred comes in. We will create a workflow to run that bash script and print it out for me. I'll let you look into how to make an Alfred workflow.

Finally, we create a Yas snippet that'll fill most of the structure. We will add a part where we can do input, and in that input, we will put in the week number.
 
 
```
# -*- mode: snippet -*-
# name: weekly template 
# key: weekly 
# --
* ------ Week $1 ------

#+BEGIN: clocktable :scope subtree :maxlevel 6 :block 2020-W$1 :step week
#+END: clocktable
** Tasks
*** TODO $0
** Notes
```
The $1 puts the cursor next to the word Week and on the block section of the clocktable. When you press enter, it moves the cursor to the TODO line.
 
I'm sure there's a way to shorten the amount of work I have to do where the week number gets set automatically, but this way it takes so little time to add a new entry that I'm not super pressed to update it.  
 
# References
 * [clocktable](https://orgmode.org/manual/The-clock-table.html)
 * [yas snippets](https://github.com/joaotavora/yasnippet)
 * [emacs](https://www.gnu.org/software/emacs/)
 * [alfred](https://www.alfredapp.com/)
 * [bash date](https://man7.org/linux/man-pages/man1/date.1.html)