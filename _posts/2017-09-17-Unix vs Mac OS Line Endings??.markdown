---
layout: post
title: "Unix vs Mac OS Line Endings"
date:   2017-09-17 14:09:00 -0700
categories: Other
---
I don't think many people have encountered this issue, but in certain cases, using Unix or Mac OS line ending can make a huge difference!

Since they're both Line Feed (LF, '\n'), if you search for '\n' (need to click to regex option) in some text editor like Sublime, you can't really tell any difference. The search result is entirely the same.

It can cause an issue if you app is splitting an input file simply by '\n', and that brought some trouble when I was trying to import a tab-delimited text file of eligible voters, converted from an Excel file on Mac OS. Based on my experience, the txt automatically has Mac OS line endings, as shown in sublime. And our PHP voting app can't reading anything other than the first line. The brief solution was to choose 'View -> Line Endings -> Unix' in Sublime.

I did a brief search on Google, and it seems currently Mac OS and Unix are both using exactly one LF character as new line. Maybe it was because our voting app was hosted on an Ubuntu server? But what exactly was changed by choosing Unix line endings instead of Mac OS line endinds? I'm really confused. Maybe I'll do some more research on this when I have more time.
