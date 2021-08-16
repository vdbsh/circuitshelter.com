+++
date="2021-08-16T18:08:53Z"
title="backy: Tiny multiprocessing utility for file backups"
description="Uncomplicated solution for 3-2-1 backups"
categories=["servers", "code"]
tags=["servers", "code", "golang", "backup"]
cover="/img/floppy_drive.png"
+++

## Sometimes the best option is the simplest one. 

If you need something to reliably sync and archive files without unnecessary integrations and complicated logic this can be your thing. 

No external dependencies or service authorizations, friendly CLI and small code base that you can read and understand. 

This tool also can be used as a complementary solution for cloud agents like Dropbox or Google Drive (e.g. continuously archive directories to cloud folder). 

Comes with install script for [Launchd](https://support.apple.com/guide/terminal/script-management-with-launchd-apdc6c1077b-5d5d-4d35-9c19-60f2397b2369/mac) in case you plan to natively schedule backup tasks for macOS 10.4+.

**Features**

* Directories synchronization
* Full directories archiving: hourly, daily, weekly, monthly or yearly with auto re-archivation if archive lost or corrupted
* Using native rsync(rsync over SSH supported) and tar(+bzip2) tools from your OS
* No third-party dependencies
* Linux, macOS and *BSD supported

**https://github.com/vdbsh/backy**