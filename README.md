# HLClock

`Time is an illusion. – Albert Einstein`

![](HLClock/Assets/time.jpg?raw=true "HLClock")

Hybrid Logical Clocks for iOS.

[![CI Status](http://img.shields.io/travis/opentable/HLClock.svg?style=flat)](https://travis-ci.org/opentable/HLClock)
[![Version](https://img.shields.io/cocoapods/v/HLClock.svg?style=flat)](http://cocoapods.org/pods/HLClock)
[![License](https://img.shields.io/cocoapods/l/HLClock.svg?style=flat)](http://cocoapods.org/pods/HLClock)
[![Platform](https://img.shields.io/cocoapods/p/HLClock.svg?style=flat)](http://cocoapods.org/pods/HLClock)


## Overview

Precise clock synchronization is hard.
For mobile devices, this problem is even worse.
It can be difficult to determine ordering of events when your clocks are out of sync.

This library contains tools to deal with problems related to clock synchronization.

### Hybrid Logical Clock (HLC)

Hybrid logical clocks allow causal ordering between events, even when those events are created on multiple devices with differing clocks.

See: http://muratbuffalo.blogspot.com/2014/07/hybrid-logical-clocks.html

![](http://3.bp.blogspot.com/-akIvKFkOoPA/U9T0IFFDQsI/AAAAAAAABrQ/Bi7YfWAIaDE/s1600/counter2.png?raw=true "Hybrid Logicl Clock Example")

### Network Time

Hybrid Logical Clocks are useful when clocks differ slightly.
User controlled mobile devices may have clocks that differ by hours (due to wrong time zone settings, etc), which is outside the bounds of what HLC is designed to compensate for.

A simple option is to maintain an offset based on the Date header received with http responses.
This can be performed e.g. upon initial login so that the clock is synced when the app starts.
This should be sufficient to get the iPad's clock to within a few seconds of "true time".

Another option is to employ NTP. NHNetworkTime is one NTP implementation that may be used: https://github.com/huynguyencong/NHNetworkTime

## Usage

```Swift
import HLClock

// Create a new timestamp
let newTimestamp = HLClock.global.now()

// Update clock when receiving a new message
HLClock.global.update(message.timestamp)

```

## Example

To run the example project, clone the repo, and run `pod install` from the Example directory first.

## Installation

HLClock is available through [CocoaPods](http://cocoapods.org). To install
it, simply add the following line to your Podfile:

```ruby
pod "HLClock"
```

## Punchlist

 - [x] Implement HLC algorithm
 - [x] Make threadsafe using atomic swap
 - [x] Package as library, installable through cocoapods
 - [ ] Clock offset uses moving median
 - [ ] Add hlclock usage to example app
 - [ ] Generate UUIDv1 using HLC timestamp
 - [ ] Add quickcheck tests

## License

HLClock is available under the MIT license. See the LICENSE file for more info.
