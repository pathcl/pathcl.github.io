---
layout: post
title: Learning concurrent.futures
---


Hello out there! from now on I'll try to share my Python knowledge in this 'blog'. 
Hopefully this will become an habit and I won't have to think about it.

Problem: Get hostname for several Dell Force10 S4048

{% gist c7dc7f3ed87fd2c3957e26e8b497b856 %}

I've hardcoded a lot on purpose. It's your job to use [argsparse](https://docs.python.org/3/library/argparse.html) or whatever you want :)

If you want to add more devices edit line 61. Maybe you want to read a file and retrieve a list? or use sqlite3?

Another approach [here](https://github.com/ktbyers/netmiko/blob/develop/examples/multiprocess_example.py). 

I do recommend you to read [Fluent Python](https://www.amazon.com/Fluent-Python-Concise-Effective-Programming/dp/1491946008). Want an 
[example](https://github.com/fluentpython/example-code/blob/master/17-futures/countries/flags2_threadpool.py)?
