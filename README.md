# react-native-android-toast
Exposes Native Toast functionality from a React Native app (Testing)

Note: this is just being created by following the tutorial found here: https://cmichel.io/how-to-create-react-native-android-library

And using the github project found:
https://github.com/MrToph/react-native-android-library-boilerplate

# Steps to actually integrate this into a getting started project and see it run

This was tested using the node v10.12.0

Creating a React Native project following the instructions here:
https://facebook.github.io/react-native/docs/getting-started

Follow the steps under Building Projects with Native code but initialize the project with React Version 0.57.1 as 0.57.3 has some bugs in it at the time of this writing.

First make sure you can run the default project following their steps without any issues.  Once you can see the project run on both an Android Emulator and an iOS Emulator proceed with the following steps.

NOTE: the first time trying to run it on ios, I believe I saw something like `:CFBundleIdentifer does not exist`, but just running it a second time it went away.  Also, don't get thrown off by warnings that you may see in the console after initially running and it can take almost a minute or so for everything to compile before it actually launches the emulator the first time and deploys the app to the emulated device.  Android seems to be much quicker initially.


After the project is initialized add this project by running at the root

```
npm install --save git+https://github.com/davidfritch/react-native-android-toast.git
```

Add a `ToastAndroidExample.js` file to your project as follows:

```
/**
 * Sample React Native App
 * https://github.com/facebook/react-native
 *
 * @format
 * @flow
 */

import React, {Component} from 'react';
import {Platform, StyleSheet, Text, View, Button, Alert} from 'react-native';
import ToastA from 'react-native-android-toast'

const instructions = Platform.select({
  ios: 'Press Cmd+R to reload,\n' + 'Cmd+D or shake for dev menu',
  android:
    'Double tap R on your keyboard to reload,\n' +
    'Shake or press menu button for dev menu',
});

export default class ToastAndroidExample extends Component {
  _onPress = Platform.select({
      ios: () => {
          Alert.alert('Alert', 'You pressed me on ios!')
      },
      android: () => {
        ToastA.show('Android Toast Ran Again!', ToastA.LONG)
      }
  })

  render() {
    return (
      <View style={styles.container}>
        <Text style={styles.welcome}>Welcome to React Native!</Text>
        <Text style={styles.instructions}>To get started, edit App.js</Text>
        <Text style={styles.instructions}>{instructions}</Text>
        <Button onPress={this._onPress} title="Press me"></Button>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#F5FCFF',
  },
  welcome: {
    fontSize: 20,
    textAlign: 'center',
    margin: 10,
  },
  instructions: {
    textAlign: 'center',
    color: '#333333',
    marginBottom: 5,
  },
});
```

And then update the `index.js` file to run that component

```
/** @format */

import {AppRegistry} from 'react-native';
import ToastAndroidExample from './ToastAndroidExample';
import {name as appName} from './app.json';

AppRegistry.registerComponent(appName, () => ToastAndroidExample);
```

Then from the root of the project finally run

```
react-native run-android
```
or
```
react-native run-ios
```

You should be able to see that when the platform is Android, it executes the native Android Module that was added, and when it is ios, it just executes an alert.
