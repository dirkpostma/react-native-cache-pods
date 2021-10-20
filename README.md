# Reduce React Native iOS build times

## Introduction

Amount  of code in pods can be huge. Pods don’t change often. On CI, all pods are compiled over and over again, which is very time intensive. What if we compile Pods once and use the result over and over again? This repo contains a demo how to accomplish this.

Based on [this blogpost](https://dev.to/retyui/react-native-how-speed-up-ios-build-4x-using-cache-pods-597c)

## Presentation

https://docs.google.com/presentation/d/e/2PACX-1vTfrXqbjTRAYCABpStRknZeCX83ku_MOzGsa0ZOq7D_JPqcYxBrrc67hLOsK1RQnKV7i94zJnAmPubZ/pub?start=false&loop=true&delayms=3000