+++ 
draft = true
date = 2022-05-15T20:54:21+01:00
title = "Connect Selenium to an existing webrowser with Python"
description = "A short snippet with a brief explanation of how to use Selenium with Python to connect to an existing web browser"
slug = "conntect-to-browser-python"
authors = []
tags = ["Python","Selenium","Automation"]
categories = ["Code"]
externalLink = ""
series = []
+++

One of the first apps I made automated multiple processes required by a corporate website at work. Naturally, this website only worked in Internet Explorer. Much to my surprise, it was a blessing in disguise, as I could manipulate the DOM through the Internet Explorer’s component object model with no need for complicated libraries, I wrote this app in AHK (AutoHotKey).

This brings us to my problem, the website was updated, destroying my old app. The website now only works in chromium based browsers. From my research, there is no way to manipulate the browser via the COM interface.

A few searches later I found Selenium, an automated website testing suite. At first, I could only get this to work by launching a new browser via Selenium. Luckily, after much searching, I found that you could use experimental flags to make a Selenium interface with a pre-existing browser. Below is a snippet I’ve saved for future reference.

- This was tested with python 3.9, using selenium 4.1.5, on Microsoft Edge 101.0.1210.47.
- The web driver can be downloaded from https://developer.microsoft.com/en-us/microsoft-edge/tools/webdriver/ 
- Edge must be run with the following flag –remote-debugging-port=9222.

```python
from selenium import webdriver
from selenium.webdriver.edge.service import Service
from selenium.webdriver.edge.options import Options

def connect(path_to_driver, debugger_address, debugger_port):
    edge_options = Options()
    edge_options.add_experimental_option("debuggerAddress", f"{debugger_address}:{debugger_port}")
    service = Service(path_to_driver)
    driver = webdriver.Edge(service=service, options=options)
    return driver
```