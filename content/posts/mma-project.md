---
author: "Tristan Jumeaux"
title: "Avoid the spoil !"
date: "2021-04-25"
description: "Find out about the career of a fighter without spoiling yourself the results !"
weight: 1
tags: ["Data","Fun", "Project"]
ShowToc: true
TocOpen: true
---

As a MMA fan, I love to watch fights during my free time.
What I especially like to do is to chose a fighter and watch all his fights from the start to the end of his career.

However, the platform that I use to do this, the UFC fight pass, doesn't offer this feature. When you search for a fighter, you just have all his fights without any particular order or temporality.

Hence, I decided to build this little project !

# How

In order to complete this task, I've decided to use combine Python and BeautifulSoup, a scrapping library.

What we want to do is allow the user to type in a fighter's name and display back its fight.
So, for example, if I want to see Michael Bisping's career, I will need to scrap this (page)[http://ufcstats.com/fighter-details/2b93ebd9f5417ad2] and get the informations.

How do we get these links ? The same website offers the ability to get every fighter with a last name starting by a specific letter. For example, here is the (b)[http://ufcstats.com/statistics/fighters?char=b&page=all] webpage.
Hence, we want to constitute a dataset with every letter of the alphabet so we will have every fighter that fights or that has fought in the UFC.

So here are the main steps : 

* Create a dataset of every fighter and their link to scrap
* Search for a fighter's name
* Scrap the concerned webpage
* Display the results

# 