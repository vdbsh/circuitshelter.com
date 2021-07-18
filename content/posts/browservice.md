+++
date = "2021-07-18T06:52:50Z"
title = "Browservice"
description = "A web 'proxy' server that enables browsing the modern web on historical browsers. It works by rendering the browser viewport into images, which are then shown by a JavaScript application running on the client browser"
tags = ["things"]
cover = ""
+++

{{< youtube oI6wJbMKjoQ >}}

# How does it work?

The Browservice server uses CEF (Chromium Embedded Framework) to run a Chromium browser instance that renders the browser view into an off-screen buffer. The browser view, combined with a control UI bar, is then compressed as a PNG or JPEG image and served to the client using an embedded HTTP server. The client browser runs a JavaScript application that requests and shows the images. It also listens for keyboard and mouse events from the user and forwards them to the proxy by including them in the URLs of the image requests.

Initially, this approach of sending the whole browser view as a new image every time it changes might sound quite inefficient. However, it is surprisingly usable if the network connection between the proxy server and the client is fast (such as 100 Mbit/s Ethernet LAN). Early 00s hardware (~1 GHz CPU clock) can often surpass 10 FPS in video streaming. The performance is also tolerable on older machines if a low JPEG compression level is used and the browser window is small.

**https://github.com/ttalvitie/browservice**