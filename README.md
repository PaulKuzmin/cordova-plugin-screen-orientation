---
title: Screen Orientation
description: Set the screen orientation
---
<!--
# license: Licensed to the Apache Software Foundation (ASF) under one
#         or more contributor license agreements.  See the NOTICE file
#         distributed with this work for additional information
#         regarding copyright ownership.  The ASF licenses this file
#         to you under the Apache License, Version 2.0 (the
#         "License"); you may not use this file except in compliance
#         with the License.  You may obtain a copy of the License at
#
#           http://www.apache.org/licenses/LICENSE-2.0
#
#         Unless required by applicable law or agreed to in writing,
#         software distributed under the License is distributed on an
#         "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
#         KIND, either express or implied.  See the License for the
#         specific language governing permissions and limitations
#         under the License.
-->

# Cordova Screen Orientation Plugin

[![Android Testsuite](https://github.com/apache/cordova-plugin-screen-orientation/actions/workflows/android.yml/badge.svg)](https://github.com/apache/cordova-plugin-screen-orientation/actions/workflows/android.yml) [![Chrome Testsuite](https://github.com/apache/cordova-plugin-screen-orientation/actions/workflows/chrome.yml/badge.svg)](https://github.com/apache/cordova-plugin-screen-orientation/actions/workflows/chrome.yml) [![iOS Testsuite](https://github.com/apache/cordova-plugin-screen-orientation/actions/workflows/ios.yml/badge.svg)](https://github.com/apache/cordova-plugin-screen-orientation/actions/workflows/ios.yml) [![Lint Test](https://github.com/apache/cordova-plugin-screen-orientation/actions/workflows/lint.yml/badge.svg)](https://github.com/apache/cordova-plugin-screen-orientation/actions/workflows/lint.yml)

Cordova plugin to set/lock the screen orientation in a common way for iOS, Android, and windows-uwp.  This plugin is based on [Screen Orientation API](http://www.w3.org/TR/screen-orientation/) so the api matches the current spec.

The plugin adds the following to the screen object (`window.screen`):

```js
// lock the device orientation
.orientation.lock('portrait')

// unlock the orientation
.orientation.unlock()

// current orientation
.orientation
```
## My FIX

In Android source added try/catch.

## Install


```bash
cordova plugin add cordova-plugin-screen-orientation
```

## Supported Orientations

#### portrait-primary
> The orientation is in the primary portrait mode.

#### portrait-secondary
> The orientation is in the secondary portrait mode.

#### landscape-primary
> The orientation is in the primary landscape mode.

#### landscape-secondary
> The orientation is in the secondary landscape mode.

#### portrait
> The orientation is either portrait-primary or portrait-secondary (sensor).

#### landscape
> The orientation is either landscape-primary or landscape-secondary (sensor).

#### any
>  orientation is  unlocked - all orientations are supported.

## Usage

```js
// set to either landscape
screen.orientation.lock('landscape');

// allow user rotate
screen.orientation.unlock();

// access current orientation
console.log('Orientation is ' + screen.orientation.type);
```

## Events

Both android and iOS will fire the orientationchange event on the window object.
For this version of the plugin use the window object if you require notification.


### Example usage

```js
window.addEventListener("orientationchange", function(){
    console.log(screen.orientation.type); // e.g. portrait
});
```

The 'change' event listener has also been added to the screen.orientation object.

### Example usage

```js
screen.orientation.addEventListener('change', function(){
    console.log(screen.orientation.type); // e.g. portrait
});
    // OR

screen.orientation.onchange = function(){console.log(screen.orientation.type);
};

```
## Android Notes

The __screen.orientation__ property will not update when the phone is [rotated 180 degrees](http://www.quirksmode.org/dom/events/orientationchange.html).

## Windows UWP Notes

Windows store apps (windows-uwp) will only display orientation changes if the device has some sort of accelerometer.  The internal state of the "orientation" will still be kept, but the actual screen won't rotate unless the device supports it.
