# gulp-cordova-build-android

> Build the cordova project for the Android platform.

## Installation

```bash
npm install --save-dev gulp-cordova-build-android
```

## Usage

```JavaScript
var gulp = require('gulp'),
    create = require('gulp-cordova-create'),
    plugin = require('gulp-cordova-plugin'),
    android = require('gulp-cordova-build-android');

gulp.task('build', function() {
    return gulp.src('dist')
        .pipe(create())
        .pipe(plugin('org.apache.cordova.dialogs'))
        .pipe(plugin('org.apache.cordova.camera'))
        .pipe(android())
        .pipe(gulp.dest('apk'));
});
```

This plugin will build the cordova project for the Android platform.

Because the plugin returns the apk file, you can pipe it to ```gulp.dest```. This will store the ```android-debug.apk``` file
in the ```apk``` directory.

### Build a release apk

By setting release to true, the plugin will build a release version of the SDK. This will store the ```android-release-unsigned.apk```
file in the ```apk``` directory.

```JavaScript
var gulp = require('gulp'),
    create = require('gulp-cordova-create'),
    plugin = require('gulp-cordova-plugin'),
    android = require('gulp-cordova-build-android');

gulp.task('build', function() {
    return gulp.src('dist')
        .pipe(create())
        .pipe(plugin('org.apache.cordova.dialogs'))
        .pipe(plugin('org.apache.cordova.camera'))
        .pipe(android({ release: true }))
        .pipe(gulp.dest('apk'));
```

### Sign the apk

To produce a signed apk you need to pass signing options to the plugin. If you pass signing options to the plugin you do not need to
specify that it is a release build as the plugin will do a release build automatically

```JavaScript
var gulp = require('gulp'),
    create = require('gulp-cordova-create'),
    plugin = require('gulp-cordova-plugin'),
    android = require('gulp-cordova-build-android');

gulp.task('build', function() {
    return gulp.src('dist')
        .pipe(create())
        .pipe(android({storeFile: '/Path/to/key.keystore', keyAlias: 'my_alias'}))
        .pipe(gulp.dest('apk'));
});
```

When running the `build` task, it will now ask for the key store password and for the key password. When the apk is signed, it will
store the `android-release.apk` file in the `apk` directory.

## API

### android([options])

#### options

##### release

Type: `boolean`

Set the build to be a release build.

##### storeFile

*Required*  
Type: `string`

Absolute path to your key file.

##### storePassword

Type: `string`

The key store password.

##### keyAlias

*Required*  
Type: `string`

The alias of the key.

##### keyPassword

Type: `string`

The password of the key alias.

##### storeType

Type: `string`

The format of the key file. The default is to auto-detect based on the file extension.

##### releaseApk

Type: `string`

Sometimes, the `cordova build --release android` produces diferrent apk file/s instead of `android-release.apk`. Specify the apk file to be copied to the `gulp.dest()` folder by passing the release apk filename to this option.

## Related

See [`gulp-cordova`](https://github.com/SamVerschueren/gulp-cordova) for the full list of available packages.

## Contributors

- Sam Verschueren [<sam.verschueren@gmail.com>]

## License

MIT © Sam Verschueren
