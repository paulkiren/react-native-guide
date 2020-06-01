# React-Native Guide

A guide for building production-ready react-native apps, based on my personal notes.\
‼️ This is a forever-work-in-progress. don't be suprised if things are out of place or broken.

## 📓 Table of Contents

### Getting Started

- [What is React-Native?](https://github.com/joeyscarim/react-native-cheatsheet#-what-is-react-native)
- [Docs & Resources](https://github.com/joeyscarim/react-native-cheatsheet#%EF%B8%8F%EF%B8%8F-docs--resources)
- [react-native init vs Expo]()
- [Project Setup & Structure](https://github.com/joeyscarim/react-native-cheatsheet#-project-setup--structure)
- [Globals Config](https://github.com/joeyscarim/react-native-cheatsheet#-globals-config)
- [Common JS & ES6 Concepts](https://github.com/joeyscarim/react-native-cheatsheet#-common-js--es6-concepts)

### Development Environment

- [Tooling](https://github.com/joeyscarim/react-native-cheatsheet#-common-js--es6-concepts)
- [Dev Environment](https://github.com/joeyscarim/react-native-cheatsheet#-dev-environment)
- [Bash Scripts](https://github.com/joeyscarim/react-native-cheatsheet#-bash-scripts)
- [Debugging]
- [Testing]

### React Concepts, State Management, Middleware

- [Hooks](https://github.com/joeyscarim/react-native-cheatsheet#-state-management-persistance-and-middleware)
- [Redux](https://github.com/joeyscarim/react-native-cheatsheet#-state-management-persistance-and-middleware)
- [Persistance](https://github.com/joeyscarim/react-native-cheatsheet#-state-management-persistance-and-middleware)
- [Middleware](https://github.com/joeyscarim/react-native-cheatsheet#-state-management-persistance-and-middleware)

### Packages

- [Yarn vs. NPM]
- [Package Management w/ NPM](https://github.com/joeyscarim/react-native-cheatsheet#-package-management-w-npm)
- [Production Ready Packages](https://github.com/joeyscarim/react-native-cheatsheet#-production-ready-packages)

### Features

- [Push notifications]
- [Video player](https://github.com/joeyscarim/react-native-cheatsheet#-video-player)
- [Chromecast](https://github.com/joeyscarim/react-native-cheatsheet#chromecast)
- [Disable font scaling](https://github.com/joeyscarim/react-native-cheatsheet#disable-font-accessibility-scaling)
- [Deep linking](https://github.com/joeyscarim/react-native-cheatsheet#disable-font-accessibility-scaling)
- [Alternate App Icons (iOS Only)](https://github.com/joeyscarim/react-native-cheatsheet#-alternate-app-icons-ios-only)

### Troubleshooting

- [Common Errors](https://github.com/joeyscarim/react-native-cheatsheet#-common-errors)
- [Reset iOS and Android directories](https://github.com/joeyscarim/react-native-cheatsheet#-reset-ios-and-android-directories)

### Publishing

- [Icons & App Store Images](https://github.com/joeyscarim/react-native-cheatsheet#-icons--app-store-images)
- [Testing](https://github.com/joeyscarim/react-native-cheatsheet#-testing)

# Getting Started

## 🤔 What is React-Native?

- React-Native is a framework for creating cross-platform native iOS and Android apps using React. One codebase, 2 mobile apps. React-Native is great for apps that **don't rely heavily on low-level API's**. i.e. an AR, VR, Camera, or bluetooth-heavy app would not be a good match for React-Native.
- React-Native has some competition, like Flutter. **Currently, I strongly believe that React-Native is the best choice for cross-platform development**. React-Native has a massive community, a ton of support from major players like Facebook, Wix, etc. and is seeing more and more adoption.
- React-Native gets some hate: https://www.youtube.com/watch?v=NxJCSI7a8wk But always consider the context. React-Native is A+ for a small team making CRUD/more basic apps. It's not designed for YouTube or Instagram to use it fully.
- React-Native is **NOT** a hybrid app tool, like Ionic. React-Native apps utilize the device API's via "bridges", instead of using a browser layer like Ionic. This gives React-Native much better performance, and direct access to any and all exposed API's.
- **Full native is always better**, in terms of flexibilty, performance, and scale. However, time and price need to be addressed also. React-Native has a nice balance of all considerations.

## 🕵️‍♂️ Docs & Resources

- Offical docs & blog: https://facebook.github.io/react-native/
- Discord: https://www.reactiflux.com/
- **(NEW!)** React Native Crash Course 2020 by Travery Media: https://www.youtube.com/watch?v=Hf4MJH0jDb4
- React JS Crash Course - 2019 by Traversy Media: https://www.youtube.com/watch?v=sBws8MSXN7A
- General resources: - Flexbox guide: https://medium.com/wix-engineering/the-full-react-native-layout-cheat-sheet-a4147802405c

## react-native-init vs. Expo

- react-native-init: - The "normal" way to create a react-native app - Full react-native experience
- Expo: - has limitations: https://docs.expo.io/versions/latest/introduction/why-not-expo/ - No IAP, bluetooth, etc. support - Must be connected to internet while developing - Doesn't support "linked" packages (some third party packages can't be used)
- **The bottom line:** Expo is awesome, but its not ready for most production use yet.

## 🚧 Project Setup & Structure

- Create a project:

```
npx react-native init MyAppName
```

- Project structure:

```
* App.js // root component
* src
 * assets // logos, images, sound effects
 * common // shared components
 * config // globals
 * lib // in-house, biz logic
 * redux // reducers, actions, store
 * screens // containers for each route
 * App.js // route stacks and app container
```

- Updating react-native:

```
react-native upgrade
```

## 🌍 Globals Config

Globals file structure:

```
// Globals.js
const mode = 'DEV';
const ver = '1.0.0'; //SEMVER

// setup env
let env = {
  MODE: mode,
  VERSION: ver
};

if (mode === 'DEV') {
  // DEV ENV
  env.API = 'https://dev.yourAPI.com/api/json/1.0/';
  // anything else you need for dev
} else {
  // PROD ENV
  env.API = 'https://yourAPI.com/api/json/1.0/';
  // anything else you need for prod
}

export default env;
```

## 🍎 Common JS & ES6 Concepts

These are the most common JS concepts that you will see throughout any React or React-Native project.

- (Fat) Arrow functions

```
// Shorthand function that automatically binds this
let combined = (string1, string2) => { return string1 + ' ' + string2 };
```

- Template literals/strings

```
let fruit1 = 'apple';
let fruit2 = 'banana';

// without template literals
console.log(fruit1 + ' ' + fruit2);

// with template literals
console.log(`${fruit1} ${fruit2}`);
```

- Higher-order functions: map, filter, forEach, reduce

```
// Functions that take functions as arguments or return functions

// Map: apple a function to each value in an array
[{i: 0, title: 'a'}, {i: 1, title: 'b'}, {i: 2, title: 'c'}].map(item => item.title);
// ["a", "b", "c"]

// Filter: filter out certain values in an array
[{i: 0, title: 'a'}, {i: 1, title: 'b'}, {i: 2, title: 'c'}].filter(item => item.title === 'a');
// {i: 0, title: "a"}

// forEach: loop over each value in an array
['a', 'b', 'c'].forEach(el => {
  console.log(el);
});
// a b c

// Reduce: reduce an array to a single object
[0, 1, 2, 3].reduce((total, current) => {
  return total + current;
}, 0);
// 6

```

- Destructuring

```
// Make copy of items from object & assign to variable
let { navigation } = this.props;
navigation.goBack();
```

- Let & Const

```
// variable identifiers, safer than var
const LIST_ITEM_HEIGHT = 200; // immutable reference, can't be reassigned
let iconColor = '#FF0000'; // block scoped, can be reassigned, helps avoid problems with closures
```

- Ternary

```
// shorthand conditional statement, useful in JSX
let someSwitch = true;
someSwitch ? console.log('on') : console.log('off');
```

- Spread syntax

```
// Allows an iterable to "spread"/expand
let object = {id: 18, name: "My Object", nickname: "obji"}
// {id: 18, name: "My Object", nickname: "obji"}
let updatedObject2 = Object.assign({...object, nickname: 'myobj'}, {});
// {id: 18, name: "My Object", nickname: “myobji”}
```

- Promises & Async/Await

```
// create a promise
let promise = new Promise((resolve, reject) => {
  // perfrom asyc call
  let success = true;
  (success ? resolve('success') : reject('error'));
 });

// call a promise
promise.then((result) => {
  console.log(result);
}, (err) => {
  console.log(err);
});
```

- Import

```
// used in place of require
import { Platform, Linking } from 'react-native';
```

# React Concepts

## Hooks

Function components come with no state at all, but the useState hook allows us to add little nuggets of state as we need them. So if all we need is a single boolean, we can create a bit of state to hold that.

- DONT replace classes. Theyre just a new option
- Allow you to add state to a functional component

`import React, { useState } from 'react';`

Resources:

- https://daveceddia.com/intro-to-hooks/
- https://daveceddia.com/intro-to-hooks/#rules-of-hooks

The useState hook takes the initial state as an argument (we passed false) and it returns an array with 2 elements: the current state, and a function to change the state.

— start playing with google play subscriptions
— see what data is returned

## Immutability / Immer

- React state should be treated as immutable
- setState, Immer, Spread, Object.assign()
- Easier debugging, safer updates, rerendering

## Suspense

" the new feature allows you to defer rendering part of your application tree until some condition is met (for example data from an endpoint or a resource is loaded)."
https://medium.com/@baphemot/understanding-react-suspense-1c73b4b0b1e6

## Context API

"Context provides a way to pass data through the component tree without having to pass props down manually at every level."
https://reactjs.org/docs/context.html

## Redux

## Class based vs functional components

(coming soon)

## Higher Order Components (HOCs)

(coming soon)

# Development Environment

## 🧰 Tooling

My preferred tools for React-Native development:

- [VS Code](https://code.visualstudio.com/) + the following extensions:
  _ Prettier
  _ ES7 React/Redux/GraphQL/React-Native snippets
  _ Bracket Pair Colorizer
  _ VSCode Great Icons
  _ Live Server
  _ Turbo Console Log \* I remap `Display` to: `shift + alt + l` in `Code -> Preferences -> Keyboard Shortcuts`
- Xcode, latest, comes installed on Mac
- [Android Studio](https://developer.android.com/studio) for Android SDK and emulation
- [Postman](https://www.getpostman.com/) for API testing
- [SourceTree](https://www.sourcetreeapp.com/) for Github management

## ⛰ Dev Environment

- Run in iOS Simulator

1. `react-native run-ios` from the project root
2. OR `react-native run-ios --simulator=“iPhone X”`
   - Options include: iPhone 5s, iPhone 6, iPhone X, iPhone 8, etc.

- Run in Android emulator

1. Open Android Studio
2. Open a blank project
3. Go to Tools -> SDK Manager -> Launch an emulator
4. `react-native run-android` from the project root

- Run on connected Android devices

1. Plug in device
2. `adb devices`: make sure the device is listed
3. `react-native run-android` from the project root
4. Shake the device or `adb shell input keyevent KEYCODE_MENU` to display the developer menu
5. React Native Debugger will work like normal with the connected device

## 🐳 Debugging with Flipper
* Facebook’s new mobile app debugger is called Flipper: https://fbflipper.com/
* It replaces react-native-debugger/Reactotron for logging, crash reporting, viewing hooks state, and inspecting redux stores.
	* It can also launch Android emulators easily without needing to launch Android Studio or using `adb` commands in Terminal
* Flipper is automatically installed with React-Native 0.62+
* For redux support, install `flipper-plugin-reduxinspector`: https://classic.yarnpkg.com/en/package/flipper-plugin-reduxinspector
	* Install it via Flipper: View —> Manage Plugins… —> Install Plugins —> redux inspector —> install
	* You can install other Flipper plugins this way too
	* If Flipper doesn’t display redux stores: in the simulator close the app fully -> reopen it

## 📈 Bash Scripts

The bash scripts I use to speed up my development

- To edit these, turn on hidden files (`Command + Shift + Period` on Mac), and then edit `.bash_profile` in your user folder.
- `alias projectName="cd projects && cd ProjectName && code . && react-native run-ios"` // one stop shop to open a dev env
- `alias run-i8p="react-native run-ios --simulator="iPhone 8 Plus"`
- `alias run-se="react-native run-ios --simulator="iPhone SE"`
- `alias assemble-android="./gradlew assembleRelease"` // make sure you `cd` into `android` before running this one

## 📦 Package Management w/ NPM

- update packages:
- Note: will only update packages in respect to semver, to avoid breaking changes

```
npm update --save
npm update --save-dev
```

- list outdated packages

```
npm outdated
```

- Update a specific package to a specific version:

```
npm install --save package-name@0.0.0
npm install --save-dev package-name@0.0.0
```

## 🗂 State Management, Persistance, and Middleware

There are a lot of ways to handle data, state, and middleware in React. The popular options include local state, redux, hooks, and mobx. Each of these have their pros and cons. For smaller apps/apps with less data, local state and/or hooks are typically preferred. For larger, API-connected projects, Redux is the preferred way of handling state. Redux can also be combined with local state and/or hooks for smaller components.

I typically use the following packages for handling state, persistance, and middleware:

- Redux + React+redux + Redux-devtools + Redux-persist + Redux-thunk + axios
- Redux-sagas is also a popular way for handling middleware in Redux

### What is redux?

Redux is an architecture pattern for handling the flow of data in an app. It is often contrasted with the MVC pattern, another common pattern for data handling.

In Redux, you have a single "store" that houses all of your data, and data always flows in one direction. The diagram below shows how data flows in Redux:

![redux diagram](https://raw.githubusercontent.com/joeyscarim/react-native-cheatsheet/master/assets/redux.gif)

Packages:

* https://github.com/kimxogus/react-native-version-check
* React-native-shared-elements
* https://github.com/tinycreative/react-native-intercom
    * Embed intercom help center!
* React-native-snap-carousel
* React-native-tab-view


- redux for global state management
  - https://github.com/reduxjs/redux
- react-redux for react + redux bindings
  - https://react-redux.js.org/
- Redux-devtools:
- redux-thunk for redux middleware to make api calls
  - https://github.com/reduxjs/redux-thunk
- redux-persist for persisting & rehydrating stores via asycstorage
  - https://github.com/rt2zz/redux-persist
- remote-redux-devtools for using redux devtools with react-native
- Axios: https://github.com/axios/axios

Install all state management + middleware packages:

```
npm install redux --save
npm install react-redux --save
npm install --save-dev redux-devtools
npm install redux-persist --save
npm install redux-thunk --save
npm install axios --save
```

Redux resources:

- What is Redux? https://code-cartoons.com/a-cartoon-intro-to-redux-3afb775501a6
- Redux Crash Course With React by Traversy Media: https://www.youtube.com/watch?v=93p3LxR9xfM

Other options:

- Local state only
- Hooks
- mobX
- etc.

## ⏫ Upgrading to new RN versions

- Upgrade helper tool
  - https://react-native-community.github.io/upgrade-helper/
- Upgrade guide

  - https://facebook.github.io/react-native/docs/upgrading

# Features

## 🎵 Push Notifications

## 📼 Video Player

Note: This setup is based on a portrait only app, with fullscreen video playback in landscape only (android) or landscape + portrait options (ios)

- Packages
  - `react-native-video`: https://github.com/react-native-community/react-native-video - the core video player
  - `react-native-video-controls`: https://github.com/itsnubix/react-native-video-controls - video controls for Android (at time of writing this, exoplayer support is not yet finished on react-native-video package)
  - `react-native-orientation-locker`: https://github.com/wonday/react-native-orientation-locker - for locking landscape mode on Android, when fullscreen is true

iOS setup:

- no need to complete the orientation-locker setup on ios
- import and use react-native-video as reccomended
- make sure app is locked to portait only mode in xcode
- there is a bug when switching from fullscreen portait -> landscape -> portait, where the screen gets cut off. to resolve this, in node_modules/react-native-video-/ios/Video/RCTVideo.m, comment out the setFrame bounds call starting at line 708:

```
        // if (!CGRectEqualToRect(oldRect, newRect)) {
        //   if (CGRectEqualToRect(newRect, [UIScreen mainScreen].bounds)) {
        //     NSLog(@"in fullscreen");
        //   } else NSLog(@"not fullscreen");

        //   [self.reactViewController.view setFrame:[UIScreen mainScreen].bounds];
        //   [self.reactViewController.view setNeedsLayout];
        // }
```

now the app won't attempt to switch to landscape mode and back, and itll still allow the video to play in fullscreen landscape mode.

Android setup:

- Do the orientation-locker setup
- in app.js, lock your app to portait mode:

```
  componentDidMount() {
    // lock android to portrait, in video fullscreen, this is changed
    Orientation.lockToPortrait();
  }
```

- In your VideoPlayer implementation, When you enter fullscreen, lock app to landscape mode, and then back to portait mode when you exit fullscreen mode:

```
<VideoPlayer
                      source={{
                        uri: video_url,
                      }}
                      onEnterFullscreen={() =>

                          Orientation.lockToLandscapeLeft() //this will lock the view to Landscape

                      }
                      onExitFullscreen={() =>
                        Orientation.lockToPortrait()

                      }
                      disableBack={true}
                      resizeMode="contain"

                      toggleResizeModeOnFullscreen={false}

                    />
```

- For fullscreen to work, you also need to either play the video on a fullsize page, or update your view to be fullsize when you enter fullscreen mode.

## 📺 Chromecast

Package: https://github.com/react-native-google-cast/react-native-google-cast

### Install and link package:

```
npm install react-native-google-cast
react-native link react-native-google-cast
```

### iOS setup:

Add pod:<br/>
`pod 'react-native-google-cast/NoBluetooth', path: '../node_modules/react-native-google-cast/ios/`

Pod install:\
`cd ios && pod install && cd ..`.

In `AppDelegate.m` add:\

```
#import <GoogleCast/GoogleCast.h>
```

and

```
GCKDiscoveryCriteria *criteria = [[GCKDiscoveryCriteria alloc] initWithApplicationID:kGCKDefaultMediaReceiverApplicationID];
GCKCastOptions* options = [[GCKCastOptions alloc] initWithDiscoveryCriteria:criteria];
[GCKCastContext setSharedInstanceWithOptions:options];
```

### Android setup:

in app/build.gradle dependencies, add:

```
    implementation "com.google.android.gms:play-services-cast-framework:${rootProject.ext.castFrameworkVersion}"
   implementation project(':react-native-google-cast')
```

Main application:

```
import com.reactnative.googlecast.GoogleCastPackage; to the imports at the top of the file
```

Android build.grade:
`castFrameworkVersion = '16.1.2'`
  
In android Manifest add:

```
 <meta-data
        android:name="com.google.android.gms.cast.framework.OPTIONS_PROVIDER_CLASS_NAME"
        android:value="com.reactnative.googlecast.GoogleCastOptionsProvider" />
```

In settings.gradle add:

```include ':react-native-google-cast'
project(':react-native-google-cast').projectDir = new File(rootProject.projectDir, '../node_modules/react-native-google-cast/android')
```

in MainActivity add:

```
import com.facebook.react.GoogleCastActivity;
```

```
public class MainActivity extends GoogleCastActivity {
  // ..
}
```

Not sure if this will work with react-navigation yet

### Javascript:

coming sooon

## disable font accessibility scaling

In App.js:

```
import {Text, TextInput} from 'react-native';

Text.defaultProps = Text.defaultProps || {};
Text.defaultProps.allowFontScaling = false;
TextInput.defaultProps = TextInput.defaultProps || {};
TextInput.defaultProps.allowFontScaling = false;
```

## 🏙 Production Ready Packages
- Modals: react-native-modal, https://github.com/react-native-community/react-native-modal
- IAP: react-native-purchased by RevenueCat, https://github.com/RevenueCat/react-native-purchases
- Crash Reporting: Firebase Crashlytics, https://rnfirebase.io/crashlytics/usage
- Dynamic Links:
- Analytics:
- FB-SDK
- Forms: formit, https://github.com/jaredpalmer/formik



- Native Base: https://github.com/GeekyAnts/NativeBase

```
npm install native-base --save
react-native link
```

- React Navigation

```
npm install --save react-navigation
npm install --save react-native-gesture-handler@~1.0.14
react-native link react-native-gesture-handler
// + Android steps at: https://reactnavigation.org/docs/en/getting-started.html
```

- One Signal: https://github.com/geektimecoil/react-native-onesignal

```
npm install --save react-native-onesignal
react-native link react-native-onesignal
// + Android steps at: https://documentation.onesignal.com/v5.0/docs/react-native-sdk-setup
```

- Moment + React-Moment: https://github.com/headzoo/react-moment#readme

```
npm install --save moment react-moment
```

- React Native Snap Carousel
- React Native Circular Progress
- Victory Native
- React Native Fast Image (for image caching)
- React-native-elements
- styled-components
- https://www.npmjs.com/package/react-native-dark-mode
- https://github.com/expo/react-native-appearance

* Animation

- Pose
- Spring
- Animatable

## Deep linking

- Basic vs Deferred
- Branch.io, Adjust.com, Appsflyer.com, Firebase Dnyamic Links (free)

Deep link launch, works with:

- adb shell am start -a android.intent.action.VIEW -d "appname://pagename" com.appname

## Documentation

-API method stubs with description, params, and return values
-API documentation generated by API testing tool (Postman)
-Comments on functions to explain general use
-Inline comments to explain complicated logic and functionality
-Readme on web and mobile app private repositories with build and update instructions

## 📱 Alternate App Icons (iOS Only)

Package: https://github.com/idearockers/react-native-dynamic-app-icon

Notes:

- The user must manually choose the icon they want to change to
- You must show the icon changed alert

Icons:

- In the root xCode projects, create a directory called `icons`
- Add 2 files for each altnerate icon, IconName@2x.png (120 x 120 px) and IconName@3x.png (180 x 180 px)
- In `Info.plist`:

```
	<key>CFBundleIcons</key>
	<dict>
		<key>CFBundleAlternateIcons</key>
		<dict>
			<key>IconName</key>
			<dict>
				<key>CFBundleIconFiles</key>
				<array>
					<string>icons/IconName</string>
				</array>
				<key>UIPrerenderedIcon</key>
				<false/>
			</dict>
			<key>CFBundlePrimaryIcon</key>
			<dict>
				<key>CFBundleIconFiles</key>
				<array>
					<string>AppIcon</string>
				</array>
			</dict>
		</dict>
	</dict>
```

# UI, UX, Styling

## Resources

-

# Troubleshooting

## 🍝 Common Errors

- Make sure singing profile/team is set in iOS!
- Any package issue, try to remove and add all modules first: `rm -rf node_modules && npm install`
- Also, make sure to link: react-native link
- If a package doesn't link correctly for iOS: drag package's xcodeproj file to Libraries, and then link manually
- If a flatlist is losing position due to the keyboard being displayed, use the prop `disableKBDismissScroll={true}` on parent ScrollView/Content component

## Understanding the Google ecosystem

- Google Play Console - Manage app releases, app store listings, reviews, etc
- Google Developer Console - Access Google APIs
- Google Firebase - Push notifications, analytics, cloudstore, hosting, user system, etc
- Google Cloud - the "backbone" of Google firebase

## 🔌 Reset iOS and Android directories

- If you need to reset your iOS and Android projects entirely, due to linking issues, package cleanup, etc.
  _ delete iOS and Android dirs
  _ react-native eject
  _ react-native link
  _ Add back any custom code (production build process, push notification logic, app icons, splash screens, etc)

# Testing & Publishing

## Building for production

- Android, follow the guide at https://facebook.github.io/react-native/docs/signed-apk-android
- `cd android && ./gradlew assembleRelease` to create an apk / android package
- `cd android && ./gradlew bundleRelease` to create an aab / android app bundle

## 📸 Icons & App Store Images

- iOS icons: Icon set creator: https://itunes.apple.com/us/app/icon-set-creator/id939343785?mt=12
- Android icons: https://romannurik.github.io/AndroidAssetStudio/index.html
- App Store Images: App Toolkit (Paid, free for one project): https://apptoolkit.io/

## 🥽 Testing

Virtual Real-Device testing:

- Andriod, Samsung Remote Test Lab (Free): https://developer.samsung.com/rtlLanding.do
- Android, Firebase Test Lab (Free): https://firebase.google.com/docs/test-lab/
- iOS and Android, BrowserStack Interactive Mobile App Testing (Paid, free trial): https://www.browserstack.com/app-live
- iOS, Testflight

## Testing with Jest

What is Jest:

- jestjs.io
- A test runner for JavaScript created by Facebook
- Has become more popular than its competitors Mocha, chai, etc.
- Finds any files with .test.js and runs them
- Test runner, assertion library, and mocking functions

Jest Methods:

- Jest has a bunch of assertion methods
- Describe, test, require, etc.

Snapshots:

- Checks to make sure that code hasn’t changed

Resources:

- Jest Crash Course by Travery Media: https://www.youtube.com/watch?v=7r4xVDI2vho
- React Testing for Beginners by LevelUpTuts: https://www.youtube.com/watch?v=D9DdY2WmM-s

How to run Jest:

- `jest --watchAll` \* Watches and runs all `.test.js` files

Example assertion:

```
test(‘truthy test', () => {
  expect(true).toBeTruthy(); //assertion
```

Unit tests:

```
// unit tests: only tests one thing
// in this cases, tests the 'add' function
// want to test multile scenarions to avoid false positives
test('add', () => {
  const value = add(1, 2);
  expect(value).toBe(3); //assertion
  expect(value).toEqual(3);
  expect(add(0, 7)).toBeGreaterThan(2);
  expect(add(-1, 4)).toBeGreaterThanOrEqual(3);
  expect(add(-1, 5)).toBeCloseTo(4);
});
```

Integration tests:

```
// integration tests: test a function that relies on another function
// in this case, the total function calls the add function
test('total', () => {
  expect(total(5, 20)).toBe('$25');
  expect(total(-5, 20)).toEqual('$15');
});
```

Mock function:

```
// mock function
// a fake function that gives you a result
// can be sync, async, return data, etc.
// can even load a function from a dependency, and turn it into a mock
const add = jest.fn(() => 3);

// unit tests
test('add', () => {
  expect(add(1, 2)).toBe(3); //assertion
  expect(add).toHaveBeenCalledTimes(1);
  expect(add).toHaveBeenCalledWith(1, 2);
});
```
