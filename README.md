Overview
========

[![Build Status](https://travis-ci.org/swisspol/GCDTelnetServer.svg?branch=master)](https://travis-ci.org/swisspol/GCDTelnetServer)
[![Version](http://cocoapod-badges.herokuapp.com/v/GCDTelnetServer/badge.png)](http://cocoadocs.org/docsets/GCDTelnetServer)
[![Platform](http://cocoapod-badges.herokuapp.com/p/GCDTelnetServer/badge.png)](https://github.com/swisspol/GCDTelnetServer)
[![License](http://img.shields.io/cocoapods/l/GCDTelnetServer.svg)](LICENSE)

GCDTelnetServer is an embedded Telnet server for iOS and OS X based on GCD. It is available under a friendly [New BSD License](LICENSE).

Requirements:
* OS X 10.7 or later (x86_64)
* iOS 5.0 or later (armv7, armv7s or arm64)
* ARC memory management only

Getting Started
===============

Download or check out the [latest release](https://github.com/swisspol/GCDTelnetServer/releases) of GCDTelnetServer then add both the "GCDTelnetServer" and "GCDNetworking/GCDNetworking" subfolders to your Xcode project.

Alternatively, you can install GCDTelnetServer using [CocoaPods](http://cocoapods.org/) by simply adding this line to your Xcode project's Podfile:
```
pod "GCDTelnetServer", "~> 1.0"
```

Using GCDTelnetServer in Your App
=================================

```objectivec
#import "GCDTelnetServer.h"

GCDTCPServer* server = [[GCDTelnetServer alloc] initWithPort:2323 startHandler:^NSString*(GCDTelnetConnection* connection) {
  
  // Return welcome message
  return [NSString stringWithFormat:@"You are connected using \"%@\"\n", connection.terminalType];
  
} lineHandler:^NSString*(GCDTelnetConnection* connection, NSString* line) {
  
  // Simply echo back the received line
  // You could as easily execute a command and return a result as a string
  return [line stringByAppendingString:@"\n"];
  
}];
[server start];
```

Then launch Terminal on your Mac, and simply enter `telnet YOUR_COMPUTER_OR_IPHONE_IP_ADDRESS 2323` and voilà, you can communicate "live" with your app.

**GCDTelnetServer has an extensive customization API, be sure to peruse [GCDTelnetConnection.h](GCDTelnetServer/GCDTelnetConnection.h).**
