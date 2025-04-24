# Flutter DevContainer Quick Start

1. Open this folder in VS Code.
2. Reopen in container when prompted.
3. In the VS Code terminal, run:

```
cd /workspace
flutter create test_app
cd test_app
flutter doctor
flutter build apk
```

- APK will be in `build/app/outputs/flutter-apk/`.
- For emulator/device support, see the referenced manual.

duild specific versions
docker build \
  --build-arg FLUTTER_VERSION=3.19.5 \
  --build-arg ANDROID_API_LEVEL=34 \
  --build-arg BUILD_TOOLS_VERSION=34.0.0 \
  -t flutter-android:minimal .

run as web app
flutter run -d web-server --web-port=8085 --web-hostname=0.0.0.0