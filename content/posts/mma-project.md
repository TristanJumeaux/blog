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

As a MMA fan, I love watching fights during my free time.
What I especially like to do is to chose a fighter and watch all his fights from the start to the end of his career.

However, the platform that I use to do this, the UFC fight pass, doesn't offer this feature. Indeed when you search for a fighter, you just have all his fights displayed without any particular order or temporality.

This is why I have decided to build a little project !
... And this is how I faced a common problematic : string comparison. 
I wanted to make a quick article about the main algorithms that I've learned about to solve this problem.

# Context 

As Human beings, we make mistakes ! Often we mistype while writing or just make a grammatical error.
Hence, I want my script to be able to find the fighter I am referencing to when I launch my script, even though there is a small mistake!

For example, if I write _Mikal Biesping_ instead of _Michael Bisping_, I want to find it anyway.

There are several algorithms to fix this issue. Let's dive into them !

# Ratcliff-Obershelp

This first algorithm might be the most used. 
Indeed, it is embedded by default in Python now. You can access it by using the difflib SequenceMatchers module.

How does it work ?

Let's say we are going to compare these two strings : _Michael Bisping_ and _Mikal Biesping_

To begin with, the algorithm will parse both strings and find common substrings.
Here's what it would get : 

![ratcliff-obershelp](/images/ratcliff.png)

We have several matches! The matches parameters represent the starting caracters in each string and the size of the common substring.

Now that we have these indicators, the Ratcliff-Obershelp algorithm will compute a ratio with the following function

```python
def _calculate_ratio(matches, length):
    if length:
        return 2.0 * matches / length
    return 1.0
```
Here, the parameter _matches_ represents the sum of the common substring sizes and _length_ is the sum of both strings lengths.

Eventually, the ratio divides put matches at scale and divides it by the total length of both strings.

For our example, we get a ratio of (2*12)/29 which is 0.8275.

That's it for the Ratcliff-Obershelp algorithm ! 
Let's move on to Levenshtein.

# Levenshtein

# Jaro-Winkler