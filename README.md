# CatalystImageConsoleMessage
Sample project demonstrating CoreUI warning messages when creating a `UIImage` from an image file with Mac idiom from the asset catalog, while running on Catalyst.

- The project contains a single png image, located in the `Assets.xcassets` catalog.
<img width="538" alt="Screenshot 2023-02-15 at 11 00 42" src="https://user-images.githubusercontent.com/2630810/219061150-b2d6317b-e95f-45df-b305-08934ebb4753.png">

- The target is set to support running on `Mac Catalyst` with **Optimize for Mac enabled** (the latter seems to be the most important part).
- Loading the image into a `UIImage` with the designated initializer and presenting it in a `UIImageView` produces the following console messages:
```
2023-02-15 10:53:18.014394+0100 CatalystImageConsoleMessage[64253:8834791] [framework] CoreUI: _Bool CUIValidateIdiomSubtypes(NSInteger, NSUInteger *) got a device subtype '32401' that it match with idiom '7':mac. Assuming subtype should be 0 instead.
2023-02-15 10:53:18.014446+0100 CatalystImageConsoleMessage[64253:8834791] [framework] CoreUI: _Bool CUIValidateIdiomSubtypes(NSInteger, NSUInteger *) got a device subtype '32401' that it match with idiom '7':mac. Assuming subtype should be 0 instead.
2023-02-15 10:53:18.014503+0100 CatalystImageConsoleMessage[64253:8834791] [framework] CoreUI: _Bool CUIValidateIdiomSubtypes(NSInteger, NSUInteger *) got a device subtype '32401' that it match with idiom '7':mac. Assuming subtype should be 0 instead.
2023-02-15 10:53:18.014533+0100 CatalystImageConsoleMessage[64253:8834791] [framework] CoreUI: _Bool CUIValidateIdiomSubtypes(NSInteger, NSUInteger *) got a device subtype '32401' that it match with idiom '7':mac. Assuming subtype should be 0 instead.
```

Working with more than a handful of images from the catalog makes the Xcode console output borderline unreadable because of these messages. The console doesn't have an option to filter *out* messages (and in general we consider it bad practice to ignore messages on the console).

Tested on Xcode 14.2 with macOS 13.2.
This issue has been reported to Apple (FB11991656).
