---
layout: post
title: Learning concurrent.futures
---


Hello out there! from now on I'll try to share my Python knowledge in this 'blog'. 
Hopefully this will become an habit and I won't have to think about it.

Problem:

    > Get hostname for several Dell Force10 S4048


```
#!/usr/bin/env python3
import concurrent.futures
import sys
import argparse
import time

try:
    from netmiko import ConnectHandler

except ImportError:
    print('Please install netmiko module: pip3 install netmiko')
    raise

except:
    print('Unexpected error:', sys.exc_info()[0])
    raise

def process(devices):
    with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
        hostname = {executor.submit(gethostname, device): device for device in devices}
        for future in concurrent.futures.as_completed(hostname):
            device = hostname[future]
            try:
                data = future.result()
            except Exception as exc:
                print('%r generated an exception: %s' % (device, exc))
            else:
                print('[{}] {}'.format(device, data))


def gethostname(device):
    dev = {
        'device_type': 'dell_force10',
        'ip': device,
        'username': 'test',
        'secret': 'test',
        'password': 'test',
        'global_delay_factor': 0,
    }

    device = ConnectHandler(**dev)
    device.enable()
    hostname = device.send_command('show run | grep hostname')
    return hostname

if __name__ == '__main__':
    devices = ['127.0.0.1', '10.10.10.1']
    start = time.time()
    process(devices)
    print('Time taken = {0:.5f}'.format(time.time() - start))

```

I've hardcoded a lot on purpose. It's your job to use [argsparse](https://docs.python.org/3/library/argparse.html) or whatever you want :)

If you want to add more devices edit line 61. Maybe you want to read a file and retrieve a list? or use sqlite3?

Another approach [here](https://github.com/ktbyers/netmiko/blob/develop/examples/multiprocess_example.py). 

I do recommend you to read [Fluent Python](https://www.amazon.com/Fluent-Python-Concise-Effective-Programming/dp/1491946008). Want an 
[example](https://github.com/fluentpython/example-code/blob/master/17-futures/countries/flags2_threadpool.py)?