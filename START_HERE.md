# FitAI: Do This Now

This is the simple path to see FitAI live.

## 1. Preview The Design

Open:

```text
preview/index.html
```

This preview is only for design. The real app is the Flutter app.

## 2. Install These Tools

Install:

- Flutter SDK
- Android Studio
- Node.js
- Firebase CLI

Then open PowerShell inside this folder:

```powershell
cd "C:\Users\sriha\OneDrive\Desktop\HARSHA\fitness app"
```

Check Flutter:

```powershell
flutter doctor
```

## 3. Connect Firebase

Create a Firebase project at:

```text
https://console.firebase.google.com
```

Enable:

- Authentication > Email/Password
- Firestore Database
- Hosting

Install tools:

```powershell
dart pub global activate flutterfire_cli
npm install -g firebase-tools
firebase login
```

Connect this app:

```powershell
flutterfire configure
firebase use --add
```

## 4. Run App On Your Computer

```powershell
flutter pub get
flutter run -d chrome --dart-define=OPENAI_API_KEY=YOUR_OPENAI_KEY
```

For Android phone/emulator:

```powershell
flutter run --dart-define=OPENAI_API_KEY=YOUR_OPENAI_KEY
```

## 5. Deploy Live Website

Build:

```powershell
flutter build web --release --dart-define=OPENAI_API_KEY=YOUR_OPENAI_KEY
```

Deploy:

```powershell
firebase deploy --only hosting,firestore:rules
```

Firebase will give you a live link like:

```text
https://your-project-id.web.app
```

That is your live FitAI web app.

## 6. Build Android App For Google Play

```powershell
flutter build appbundle --release --dart-define=OPENAI_API_KEY=YOUR_OPENAI_KEY
```

Upload this file to Google Play Console:

```text
build/app/outputs/bundle/release/app-release.aab
```

## Important

For a real public app, do not keep OpenAI calls directly inside the mobile app forever. The safest production setup is Firebase Cloud Functions calling OpenAI, because public apps can expose client-side API keys.

## Separate Customer And Admin Layouts

FitAI has two different layouts after login.

Customer layout:

- Home
- Workout
- Diet
- Profile

Admin layout:

- Dashboard
- Users
- Controls

Admins do not see the customer bottom navigation. Customers do not see admin screens.

The Admin layout lets you:

- See total customers
- See registered customer profiles
- Turn Workout AI on/off
- Turn Diet AI on/off
- Turn Chat Coach on/off
- Enable maintenance mode
- Save a customer notice

To make yourself admin after signing up:

1. Open Firebase Console.
2. Go to Authentication and copy your user UID.
3. Go to Firestore Database.
4. Open `users/{yourUid}`.
5. Change `role` from `user` to `admin`.
6. Create a new document:

```text
admins/{yourUid}
```

Add any field, for example:

```text
createdAt: current timestamp
```

7. Deploy rules:

```powershell
firebase deploy --only firestore:rules
```

8. Log out and log in again. You will see the Admin tab.
