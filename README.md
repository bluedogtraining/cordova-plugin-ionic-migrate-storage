# `cordova-plugin-ionic-migrate-ios-storage`

Specific fixes to the original fork, allowing migration of file:// (no hostname, no port) to app://localhost LocalStorage. This probably isn't useful to anyone else.



> Cordova plugin that migrates localStorage data from cordova-plugin-ionic-webview@1.X.X to cordova-plugin-ionic-webview@4.X.X and above. This works for iOS only!

## Installation

Straight forward, just via `cordova plugin add`.

```
cordova plugin add --save cordova-plugin-ionic-migrate-ios-storage@0.3.6
```

This work is forked from https://github.com/pointmanhq/cordova-plugin-ionic-migrate-ios-storage, which migrates IndexedDB, LocalStorage, and WebSQL from cordova's default UIWebView to cordova-plugin-ionic-webview. We needed to migrate not from the default UIWebView, but from cordova-plugin-ionic-webview@1.X.X to cordova-plugin-ionic-webview@4.X.X, and only localStorage was needed, so IndexedDB and WebSQL support were removed and the migration locations were made configurable. Theoretically, this plugin could also be used to migrate from UIWebView to cordova-plugin-ionic-migrate-ios-storage. The following settings are configurable (defaults listed):
This work is forked from https://github.com/pointmanhq/cordova-plugin-ionic-migrate-ios-storage, which migrates IndexedDB, LocalStorage, and WebSQL from cordova's default UIWebView to cordova-plugin-ionic-webview. We needed to migrate not from the default UIWebView, but from cordova-plugin-ionic-webview@1.X.X to cordova-plugin-ionic-webview@4.X.X, and only localStorage was needed, so IndexedDB and WebSQL support were removed and the migration locations were made configurable. Theoretically, this plugin could also be used to migrate from UIWebView to cordova-plugin-ionic-migrate-ios-storage. The following settings are configurable (defaults listed):

#define DEFAULT_TARGET_HOSTNAME @"localhost"
#define DEFAULT_TARGET_SCHEME @"ionic"
#define DEFAULT_TARGET_PORT_NUMBER @"0"

#define DEFAULT_ORIGINAL_HOSTNAME @"localhost"
#define DEFAULT_ORIGINAL_SCHEME @"http"
#define DEFAULT_ORIGINAL_PORT_NUMBER @"8080"

```xml
<!-- cordova-plugin-ionic-webview@4.x.x defaults to serving from http://localhost on Android and ionic://localhost on iOS -->
<preference name="Scheme" value="http" />
<preference name="iosScheme" value="ionic" />
<preference name="Hostname" value="localhost" />
<preference name="WKPort" value="" />

<!-- cordova-plugin-ionic-webview@1.x.x defaults to serving from http://localhost:8080 -->
<preference name="MIGRATE_STORAGE_ORIGINAL_SCHEME" value="http" />
<preference name="MIGRATE_STORAGE_ORIGINAL_HOSTNAME" value="localhost" />
<preference name="MIGRATE_STORAGE_ORIGINAL_PORT_NUMBER" value="8080" />
```


## Testing

To test this, you will have to do the following:

* Delete the app from your device
* Remove the webview and migrate plugins from your app:

```
cordova plugin rm --save cordova-plugin-ionic-webview @kassamina/cordova-plugin-ionic-migrate-ios-storage
```

* Build your app and run it. Store something in localStorage, WebSQL and IndexedDB.
* Add the plugins back:
        
```
cordova plugin add --save cordova-plugin-ionic-webview@4.1.3 cordova-plugin-ionic-migrate-ios-storage@0.3.6
```

* Build your app and run it. The stored data must all exist!

## Caveats / Warnings / Gotchas

* Until the plugin reaches `v.1.0.0`, breaking changes will be introduced in every minor version upgrade! Use one of [the tags listed here](https://github.com/kassamina/cordova-plugin-ionic-migrate-storage/releases) if you want to lock it down to a specific changeset.
* **This has only been tested with  `ios`, migrating from `cordova-plugin-ionic-webview@1.2.1` to `cordova-plugin-ionic-webview@4.1.3`!**
* Currently, this plugin does not work on simulators. PRs welcome!
* This copy is uni-directional, from old webview to new webview. It does not go the other way around. So essentially, this plugin will run only once! 

## Thanks

Most of the code in this plugin was either adapted or inspired from a plethora of other sources. Creating this plugin would not have been possible if not for these repositories and their contributors:

* https://github.com/styleseat/cordova-plugin-ionic-migrate-storage
* https://github.com/pointmanhq/cordova-plugin-ionic-migrate-storage
* https://github.com/jairemix/cordova-plugin-migrate-localstorage/
* https://github.com/MaKleSoft/cordova-plugin-migrate-localstorage
* https://github.com/Telerik-Verified-Plugins/WKWebView/
* https://github.com/ccgus/fmdb
* https://github.com/jacek-marchwicki/leveldb-jni

## TODO 

* Pull out debug flags to make them platform specific and not rely on booleans in the code.
* Add some unit testing.
* Open source stuff - github issue templates, CONTRIBUTING doc, Local development doc etc.
