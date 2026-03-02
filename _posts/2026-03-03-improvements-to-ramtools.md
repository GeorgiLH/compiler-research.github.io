---
title: "Making improvements to the ramtools project"
layout: post
excerpt: "Understanding the inner workings of rntuple and ways to improve efficiency"
sitemap: false
author: Georgi Haralanov
permalink: blogs/ramtools_Georgi_Haralanov_blog/
date: 2026-03-02
tags: c++ genomics bioinformatics cern root rntuple 
---

{% include dual-banner.html
left_logo="/images/mg-pld-logo.png"
right_logo="images/cr-logo-old.png
caption=""
height="20vh" %}

## Introduction
My name is Georgi Haralanov and I will be working on making the Ramtools
project faster

**Mentor**: Vassil Vassilev

## Overview

The Ramtools project aims to bring the columnar file format of RNTuple from
the field of high-energy physics to the storage of genomic data. This has already
been established with convertor scripts from SAM to RNTuple format and reader
applications which allow the view of the RNTuple files. This has shown great promise
as the performance of these tools is by far the best when looking at large data samples
which are common in the field of bioinformatics.

## Current performance
When analyzed with tools such as **samply** the performance of the current iterations
of the tools shows that individual calls of functions are very optimized and fast
but the sheer amount of data that needs to be scanned adds to the delay in the
execution of the code.

## Possibilities for improvements
One way to achieve faster times is by employing multiple parallel processes to
search through the file. This has already been implemented by the project in
a certain way. By fragmenting the file into multiple ones each containing a single
chromosome and spawning a process for each of those files we can achieve multithreading
when searching over multiple chromosomes. But this approach stops working when we want
to view only one chromosome. By multithreading a single process we can decrease query
times no matter the set search space.

## Possible implementations
I intend to look at two different implementations:
1. The built-in ROOT implementation of implicit multithreading (IMC):
Using the built in ROOT IMC we can stick close to the already established framework
and maintain compatibility.
2. C++ implemented multithreading
The ROOT implementation some features which might not lead to a significant decrease
in speeds on certain platforms and/or use cases. Thats why I plan to research a
personal implementation of the multithrading functionality.

## Project goals
1.Set up a benchmark to check and record current speeds
2.Implement the built-in IMC
3.Benchmark that implementation
4.Implement personal multithreading
5.Benchmark personal one
6.Compile findings and publish results

## Expected results
Per-process multithreading combined with multi-process viewing of a single file
could lead to multiple times decrease in query times especially when looking at
large cross-chromosome level searching. With the increase of data in the field
this would be a welcome improvement to the workflow of large scale analysis
laboratories.
