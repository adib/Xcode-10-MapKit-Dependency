# Xcode-10-MapKit-Dependency

This is a sample project demonstrating an issue in which Xcode 10.0 inadvertently creates dependency to MapKit.

When Xcode 10 builds a Swift macOS project including a Photo Editing extension, it always adds a dependency to MapKit, even when the main app and the app extension does not make use of maps functionality.


## Steps to Reproduce

1. Create a single-window macOS application with Swift 4.2 as the programming language (use the sample template from Xcode).
2. Add a Photos Editing extension to the app.
3. Build the application on macOS High Sierra.
4. Inspect the built application and see its `Frameworks` folder.

Alternatively for steps 1..2 use the sample project in the `TestApp` folder.

## Expected Results

Since this is essentially a “blank application”, the dependencies should be minimal.  Specifically the app **must not** have any dependency to the MapKit framework.

## Actual Results

Xcode includes `libswiftMapKit.dylib` into the application bundle’s `Frameworks` directory. In turn this forces the app to have a dependency to MapKit and causes App Store review rejection if the app does not have maps functionality.

Forcibly removing the `libswiftMapKit.dylib` library would cause the Photo Editing Extension to stop functioning. 


## Environment

- Xcode version 10.0 (10A255)
- macOS High Sierra version 10.13.6 (17G65)
- Swift 4.2

## Notes

This was current as of 21 September 2019.


Contact:
> Sasmito Adibowo  
> https://cutecoder.org


