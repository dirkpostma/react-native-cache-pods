# Reduce React Native iOS build times

## Introduction

Amount  of code in pods can be huge. Pods don’t change often. On CI, all pods are compiled over and over again, which is very time intensive. What if we compile Pods once and use the result over and over again? This repo contains a demo how to accomplish this.

Based on [this blogpost](https://dev.to/retyui/react-native-how-speed-up-ios-build-4x-using-cache-pods-597c)

## Demo

- clone this repo
- run `yarn install`
- `cd ios`
- run `pod install`
- run `gem install` (?)
- run `bundle exec fastlane ios cached_build` for first time
- check build time, and notice existens of folder `cached_derived_data`
- run `bundle exec fastlane ios cached_build` again
- check build time

If everything worked well, you'see a drastically smaller build time the second time.

First build, without cache:
```
+------+------------------+-------------+
|           fastlane summary            |
+------+------------------+-------------+
| Step | Action           | Time (in s) |
+------+------------------+-------------+
| 1    | default_platform | 0           |
| 2    | gym              | 384         |
+------+------------------+-------------+
```

Second build:
```
+------+------------------+-------------+
|           fastlane summary            |
+------+------------------+-------------+
| Step | Action           | Time (in s) |
+------+------------------+-------------+
| 1    | default_platform | 0           |
| 2    | gym              | 63          |
+------+------------------+-------------+
```

## CI

On CI, you can do the followwing in your build script:

1. first try to download `<md5 of Podfile.lock>.zip` from your favorite storage system (Azure Storage, S3 bucket, FTP, etc...)
2. If success, unzip into `ios/cached_derived_data`
3. Run `bundle exec fastlane ios cached_build`
4. If `<md5 of Podfile.lock>.zip` didn't exist, zip `cached_derived_data` and upload it somewhere as `<md5 of Podfile.lock>.zip`

This way, only when `Podfile.lock` changes, Pods will be compiled.

## Presentation

https://docs.google.com/presentation/d/e/2PACX-1vTfrXqbjTRAYCABpStRknZeCX83ku_MOzGsa0ZOq7D_JPqcYxBrrc67hLOsK1RQnKV7i94zJnAmPubZ/pub?start=false&loop=true&delayms=3000