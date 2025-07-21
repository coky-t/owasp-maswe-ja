---
title: 実装されていない Device Attestation (Device Attestation Not Implemented)
id: MASWE-0100
alias: device-attestation
platform: [android, ios]
profiles: [R]
mappings:
  masvs-v1: [MSTG-RESILIENCE-10]
  masvs-v2: [MASVS-RESILIENCE-1]
  cwe: [693]

refs:
- https://developer.android.com/google/play/integrity
- https://support.google.com/googleplay/android-developer/answer/11395166?hl=en
- https://www.youtube.com/watch?v=TyxL78e5Bag
- https://github.com/1nikolas/play-integrity-checker-app
- https://developer.apple.com/videos/play/wwdc2021/10244/ 
- https://developer.apple.com/documentation/devicecheck/preparing-to-use-the-app-attest-service 
- https://github.com/iansampson/AppAttest 
- https://github.com/firebase/firebase-ios-sdk/blob/v8.15.0/FirebaseAppCheck/Sources/AppAttestProvider/DCAppAttestService%2BFIRAppAttestService.h 
- https://blog.restlesslabs.com/john/ios-app-attest
draft:
  description: The app doesn't use App Attestation APIs, such as Google Play Integrity API, iOS DeviceCheck API,so the backend cannot ensure requests originate from a genuine app binary (CWE-693). This exposes the app to tampering, fraud, replay attacks, and unauthorized use of premium features.
  topics:
  - detection in place
  - Effectiveness Assessment (e.g. bypassing the detection)
status: placeholder

---
