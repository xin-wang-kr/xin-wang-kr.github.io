---
title: Regular expressions for replication
date: 2021-07-01
permalink: /posts/2021/07-rstudio-regex
excerpt: "My research"
toc: true
tags:
  - regex
---

As part of the publication process for my recent [article](https://doi.org/10.1177/07388942211015242) on how states preempt separatist conflict, I needed to submit replication materials to the journal. I took my graduate quantitative methods sequence with the late [Tom Carsey](https://sites.google.com/view/tom-carsey/home), so I've long been a proponent replicability efforts in social science. I also had an hourly job in grad school replicating quantitative results for multiple political science journals, so I'm very familiar with best practices for replication. Unfortunately, in the four years since I wrote the first line of code for this project, somewhere in between defending my dissertation and starting a new job (ok, fine, almost immediately after writing that first line of code), I got a little lazy.


Sometimes it's faster (easier) to just write code that works for you, on your system, without any consideration for some poor researcher who may try to replicate your results in the future.[^replication] This tendency was especially bad for this project because at various points in time I was writing code to run on my personal laptop and [two](https://its.unc.edu/research-computing/killdevil-retirement/) [different](https://its.unc.edu/research-computing/longleaf-cluster/) high performance computing clusters. This is a recipe for code that doesn't travel well and will almost certainly fail to replicate.
