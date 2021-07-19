+++
date = "2021-07-19T14:30:00Z"
title = "Checking host availability with Python and AWS Lambda"
description = "How to check host availability from AWS Lambda with minimal footprint"
tags = ["servers", "code", "aws", "lambda" , "python"]
categories = ["servers", "code"]
cover = ""
+++

[AWS Lambda](https://aws.amazon.com/lambda/) is great for quick and straightforward tasks without any unnecessary functions complications.
But Sometimes you need to optimize your approach even for such simple task as checking host availability to make it as fast and minimal as possible.

For this task we are going to use [Low-level networking interface from Python 3](https://docs.python.org/3/library/socket.html) to try establish connection directly to remote socket without help of any additional protocols like [ICMP](https://en.wikipedia.org/wiki/Internet_Control_Message_Protocol).

```python
from socket import socket, AF_INET, SOCK_STREAM

addresses = [
    {'example.com': 80},
    {'example.com': 443},
    {'host-1234567890-notexist.example.com': 1234}]

def echo(addresses: list):
    results = {}

    for address in addresses:
        for host, port in address.items():
            try:
                s = socket(AF_INET, SOCK_STREAM)
                s.connect((str(host), int(port)))
            except OSError:
                results[f'{host}:{port}'] = False
            else:
                s.close
                results[f'{host}:{port}'] = True

    return results

def lambda_handler(event, context):
    return echo(addresses)
```