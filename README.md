# GTMPodIssueTest

Test project to illustrate issues with the latest GoogleTagManager iOS sdk version (7.3.0), when used in combination with the latest Usabilla version (6.7.1) through CocoaPods.

## How to reproduce

Checkout the code, run `pod install` (using Cocoapods 1.10.1), observe the following output:

> Analyzing dependencies
> 
> Downloading dependencies
> 
> Installing FirebaseAnalytics (8.0.0)
> 
> Installing FirebaseCore (8.0.0)
> 
> Installing FirebaseCoreDiagnostics (8.0.0)
> 
> Installing FirebaseInstallations (8.0.0)
> 
> Installing GoogleAnalytics (3.17.0)
> 
> Installing GoogleAppMeasurement (8.0.0)
> 
> Installing GoogleDataTransport (9.0.0)
> 
> Installing GoogleSymbolUtilities (1.1.2)
> 
> Installing GoogleTagManager (7.3.0)
> 
> Installing GoogleUtilities (7.4.1)
> 
> Installing GoogleUtilitiesLegacy (1.3.2)
> 
> Installing PromisesObjC (1.2.12)
> 
> Installing Usabilla (6.7.1)
> 
> Installing nanopb (2.30908.0)
> 
> Generating Pods project
> 
> Integrating client project
> 
> Pod installation complete! There are 2 dependencies from the Podfile and 14 total pods installed.
> 
> [!] Can't merge user_target_xcconfig for pod targets: ["GoogleTagManager", "Usabilla"]. Singular build setting EXCLUDED_ARCHS[sdk=iphonesimulator*] has different values.
> 
> [!] Can't merge user_target_xcconfig for pod targets: ["GoogleTagManager", "Usabilla"]. Singular build setting EXCLUDED_ARCHS[sdk=iphonesimulator*] has different values.

## Cause
GoogleTagManager contains `EXCLUDED_ARCHS` in the `user_target_xcconfig` field of its [podspec](https://github.com/CocoaPods/Specs/blob/master/Specs/9/5/6/GoogleTagManager/7.3.0/GoogleTagManager.podspec.json).

Usabilla contains the same, but with different value in its [podspec](https://github.com/CocoaPods/Specs/blob/master/Specs/0/2/3/Usabilla/6.7.1/Usabilla.podspec.json)

## Solution
Podspecs should not define `EXCLUDED_ARCHS` in the `user_target_xcconfig` fied of their podspec. 

## References
* [Similar issue in NewRelic](https://discuss.newrelic.com/t/issues-with-pod-install-related-to-excluded-archs/120131/18)
* [Similar issue](https://groups.google.com/g/ima-sdk/c/_RSd8NMYvRo) [with other Google pods](https://stackoverflow.com/a/66592995/819110)
