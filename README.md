# React Native Heading
Get device heading information on iOS or Android

## What
Report back device orientation in degrees, 0-360, with 0 being North.

#### Example
```java
const { DeviceEventEmitter } = require('react-native');
const ReactNativeHeading = require('react-native-heading');

//....
  componentDidMount() {
    ReactNativeHeading.start(1)
	.then(didStart => {
		this.setState({
			headingIsSupported: didStart,
		})
	})
	
    DeviceEventEmitter.addListener('headingUpdated', data => {
    	console.log('New heading is:', data.heading);
    });

  }
  componentWillUnmount() {
  	ReactNativeHeading.stop();
  	DeviceEventEmitter.removeAllListeners('headingUpdated');
  }
//...
```

| Version | React Native Support |
|---|---|
| 1.1.0 | 0.40.0 - 0.41.0 |
| 1.0.0 | 0.33.0 - 0.39.0 |
*Complies with [react-native-version-support-table](https://github.com/dangnelson/react-native-version-support-table)*

#### API

`start(filter)` - Start receiving heading updates. Accepts an optional filter param (int) to ignore heading changes less than the spcified threshold. The default value is 5. Returns a promise which can be used to determine if heading updates are suported by the device.

`stop` - Stop receiving heaing updates (don't forget to remove the `headingUpdated` listener)


## Setup

````
npm install --save react-native-heading
````

### iOS
* Run open node_modules/react-native-heading
* Drag ReactNativeHeading.xcodeproj into your Libraries group

### Android
##### Step 1 - Update Gradle Settings

```
// file: android/settings.gradle
...

include ':react-native-heading'
project(':react-native-heading').projectDir = new File(rootProject.projectDir, '../node_modules/react-native-heading/android')
```
##### Step 2 - Update Gradle Build

```
// file: android/app/build.gradle
...

dependencies {
    ...
    compile project(':react-native-heading')
}
```
##### Step 3 - Register React Package
```
...
import com.joshblour.reactnativeheading.ReactNativeHeadingPackage; // <--- import

public class MainActivity extends ReactActivity {

    ...

    @Override
    protected List<ReactPackage> getPackages() {
        return Arrays.<ReactPackage>asList(
            new MainReactPackage(),
            new ReactNativeHeadingPackage() // <------ add the package
        );
    }

    ...
}
```
