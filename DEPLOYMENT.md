# FitAI Live Deployment

Use Firebase Hosting for the live web app. Use Google Play Console for Android.

Render is not the best choice here because FitAI is a Flutter/Firebase app, not a Node/Express backend server.

## Fastest Live Web Deploy

```bash
flutter pub get
flutterfire configure
firebase login
firebase use --add
flutter build web --release --dart-define=OPENAI_API_KEY=sk-your-key
firebase deploy --only hosting,firestore:rules
```

Your live app will be available at:

```text
https://YOUR_PROJECT_ID.web.app
```

## Android APK

```bash
flutter pub get
flutterfire configure
flutter build apk --release --dart-define=OPENAI_API_KEY=sk-your-key
```

The APK will be created at:

```text
build/app/outputs/flutter-apk/app-release.apk
```

## Android App Bundle

Use this for Google Play:

```bash
flutter build appbundle --release --dart-define=OPENAI_API_KEY=sk-your-key
```

The bundle will be created at:

```text
build/app/outputs/bundle/release/app-release.aab
```

Before Play Store release, replace the debug signing config in `android/app/build.gradle` with your release keystore.
The Android package id is `com.fitai.app`.

## Web Hosting With Firebase

```bash
flutter pub get
flutterfire configure
flutter build web --release --dart-define=OPENAI_API_KEY=sk-your-key
firebase deploy
```

## Required Firebase Setup

- Enable Authentication > Sign-in method > Email/Password.
- Create Firestore Database.
- Deploy `firestore.rules`.
- Download Android `google-services.json` into `android/app/google-services.json`, or run `flutterfire configure`.

## Required Values

Replace placeholders in `lib/firebase_options.dart` by running `flutterfire configure`.

Never commit real API keys to public GitHub repositories. For production, move OpenAI calls into Firebase Cloud Functions.
