# CarbCalc

Proyecto Android (Kotlin + Jetpack Compose + MVVM + Room).
* compileSdk/targetSdk: 35
* minSdk: 24
* Java/Kotlin: 17 / 1.9.24

## Compilar APK

```bash
./gradlew assembleDebug
# APK: app/build/outputs/apk/debug/app-debug.apk

./gradlew assembleRelease
# APK unsigned: app/build/outputs/apk/release/app-release-unsigned.apk
```

## Firmar (manual)

```bash
keytool -genkeypair -v -keystore carbcalc.keystore -alias carbcalc -keyalg RSA -keysize 2048 -validity 3650
zipalign -f 4 app/build/outputs/apk/release/app-release-unsigned.apk app-release-aligned.apk
apksigner sign --ks carbcalc.keystore --ks-key-alias carbcalc --out app-release-signed.apk app-release-aligned.apk
apksigner verify --verbose --print-certs app-release-signed.apk
adb install -r app-release-signed.apk
sha256sum app-release-signed.apk
```

*Alternativa:* Build > Generate Signed APK en Android Studio (elige APK, no AAB).
