# PR's Welcomed


# react-native-geckowebview-and-adblock

Forked from [react-native-geckowebview-and-adblock](https://github.com/sunnylqm/react-native-geckoview)

Based on [GeckoView](https://github.com/mozilla/geckoview). Just a proof of concept.

run `yarn add https://github.com/filipef101/react-native-geckowebview-and-adblock`

Not published on npm

Android only

Autolinking

## Getting started

1. `$ yarn add react-native-geckoview`  

2. Add the following to your `build.gradle`'s repositories section. (android/build.gradle)

```gradle
allprojects {
    repositories {
      // ...
      // ...

      // ADD THIS
      maven {
          url "https://maven.mozilla.org/maven2/"
      }
    }
}
```

3. `$ yarn android`


## Usage
```javascript
import GeckoView from 'react-native-geckoview';

<GeckoView source={{ uri: 'https://www.google.com' }} />;
```
## Adblock with ublock origin
Download a "firefox.signed.xpi " from [here](https://github.com/gorhill/uBlock/releases) , rename it to zip, and extract it.
place the contents in android/app/src/main/assets/signed, so that the manifest.json ends up in android/app/src/main/assets/signed/manifest.json.

You should ocasionally update this so you get all the latest adblocking goodness.

on android/app/build.gradle

add the following under `defaultConfig { ` .  | This is because the adblock folder contains folders starting with underscore that are removed if we don't put this.
```
aaptOptions {
            ignoreAssetsPattern '!.svn:!.git:!.ds_store:!*.scc:!CVS:!thumbs.db:!picasa.ini:!*~'
        }
```

## FAQ
### Android build fails with "Java heap space" error

Make your gradle.properties look like the following:
```
android.useAndroidX=true
android.enableJetifier=true
org.gradle.jvmargs=-Xmx4g -XX:MaxPermSize=2048m -XX:+HeapDumpOnOutOfMemoryError -Dfile.encoding=UTF-8
```
And add the following in your app/build.gradle under the android task:

```
android {

  dexOptions {
    javaMaxHeapSize "4g"
  }
}  
```

### Does this send a X-requested-with header like normal webview?
No! This means a website cannot detect that it is a webview by looking for that header (will look to add custom UA if requested).
