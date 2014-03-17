---
layout: post
title: "The Secret behind NTU Matriculation Numbers"
description: "Hash Function"
category: Computer Science
tags: []
---
{% include JB/setup %}
###Matriculation Number
Every student matriculated in Nanyang Technological University Singapore (NTU) is assigned a matriculation number, in a SAMPLE format of `U1234567A`. "U" stands for type of study, thus "U" is for undergraduate student, "G" is for graduate student, and "N" is for exchange student. "12" stands for the year matriculated, thus "12" is for students matriculated in year 2012. "34" is for school code, normally "10" is for Nanyang Business School and "20" "21" are for College of Engineering. "567" is a unique identifier for every single student in a non-sequential manner. Last letter "A" is the checksum ([hash value][2]) of the matriculation number. 

NTU has changed the matriculation number format thus is different from 2005 version according to [this][1]. In this study, only "U", undergraduate, matriculation numbers are studied since I only sufficient access to such matriculation numbers.  

The pattern for digits in the matriculation numbers can be easily observed, and the pattern is as explained above. The only difficulty lies in how to calculate the checksum as the last letter. 
###Hash Function 
####Heuristic
As observed in large set of samples, the checksum letter space is `A-L` excluding `I`. Thus the size of checksum letter space is 11, a prime number which is commonly used in simple hash function. 
####Algorithmic
Searching for digit weights. Every digit's weight range from 0 to 10, since 11 is the prime number doing the hashing. There are 7 digits in matriculation number, thus there are 11^7 possibilities. A program is written to search for the digit weights. 

###Implementation
Let the hacking begin. Code is written Python and uses brutal force approach. Okay it is as slow as half-life of [Carbon-14][4].  

Audiences are not patient. Neither am I. The following simple techniques are used to speed up the process: 
* [Multiprocesss][5] parallelism 
* Python JIT compiler - [pypy][6]
* 3.4GHz dual-core [CPU][7]

####Source Code
The final program is on [GitHub][3]. 

####Produced Results 

{% highlight python %}
# checksum number to checksum letter mapping
candiates_sum = {0: "a", 1: "b", 2: "c", 3: "d", 4: "e", 5: "f", 6: "g", 7: "h", 8: "j", 9: "k", 10: "l"}
{% endhighlight %}

{% highlight python %}
# digit wights 
# 1st digit is weighted at 10, 2nd at 7, and so on. 
weight = [10, 7, 4, 3, 2, 9, 8]
offset = 0
{% endhighlight %}
###Sample Calculation
Given the sample matriculation number `U1122983C`, the `C` is calulated as followed: 

| *Code*        | *Letter*    |
| ------------- |-------------|
|0 |a|
|1 |b|
|2 |c|
|3 |d|
|4 |e|
|5 |f|
|6 |g|
|7 |h|
|8 |j|
|9 |k|
|10|l|


```
# weight = [10, 7, 4, 3, 2, 9, 8]
# matric = [1, 1, 2, 2, 9, 8, 3]
# weight dot multiplies matric

1*10+1*7+2*4+2*3+9*2+8*9+3*8 
= 145
145 mod 11
= 2
```

thus the checksum 'C'. 
###Limitations
* Do not have sufficient large sample size, only around 100 samples are tested
* Some samples have error in themselves due to manual errors. 
* Samples are biased since all the numbers starts with digit "1"


Bug reports are welcomed. If you find some errors please comments below or contact me directly.   

[1]: http://www.kejut.com/ntumatric
[2]: http://en.wikipedia.org/wiki/Hash_function
[3]: https://github.com/zhangdanyangg/MatricNumberCracker
[4]: http://en.wikipedia.org/wiki/Carbon-14
[5]: http://docs.python.org/2/library/multiprocessing.html
[6]: http://pypy.org/
[7]: http://ark.intel.com/products/52231/Intel-Core-i7-2620M-Processor-4M-Cache-up-to-3_40-GHz