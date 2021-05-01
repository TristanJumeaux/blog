---
author: "Tristan Jumeaux"
title: "Jaro-Winkler, Levenshtein & Mixed Martial Arts"
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

Hence, I have decided to build a little project.

During this project I faced a common problematic : string comparison ! 
I wanted to make a quick article about the main algorithms to solve this problem.

# Context 

To launch my script, I type the name of a fighter. You can see how it works in the following picture.

As Human beings, we make mistakes ! Often we mistype while writing or just make a grammatical error.
Hence, I want my script to be able to find the fighter I am referencing to even though there is a small mistake!

For example, if I write _Michel Bisping_ instead of _Michael Bisping_, I want to find it anyway.

There are several algorithms to fix this issue. Let's dive into them !

# Ratcliff-Obershelp

This first algorithm might be the most used. 
Indeed, it is embedded by default in Python now. You can access it by using the difflib SequenceMatchers module.

How does it work ? 





# Levenshtein

# Jaro-Winkler