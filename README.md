# FitAI

A Flutter mobile app that uses Firebase Auth, Firestore, and OpenAI to act as a practical AI personal trainer.

For the fastest setup, start with [START_HERE.md](START_HERE.md).

## Features

- Email/password login and signup
- User fitness profile with name, age, weight, and goal
- Dark Material UI with bottom navigation
- Dashboard with current goal, today's workout, and calorie summary
- AI workout generator using goal and available time
- AI diet assistant that estimates calories and suggests the next meal
- AI daily diet plan generator
- Separate customer and admin layouts
- Admin controls for AI feature availability and maintenance mode
- ChatGPT-style fitness assistant
- Progress tracking for weight and completed workouts

## Project Structure

```text
lib/
  models/       Data models for profile, workouts, diet, progress, chat
  providers/    Provider app state
  screens/      Auth, dashboard, workout, diet, chat, profile screens
  services/     Firebase Auth, Firestore, OpenAI API services
  widgets/      Reusable UI widgets
```

## Setup

1. Install Flutter and verify it:

```bash
flutter doctor
```

2. Install packages:

```bash
flutter pub get
```

3. Create a Firebase project:

- Enable Email/Password Authentication.
- Create a Firestore database.
- Install FlutterFire CLI if needed:

```bash
dart pub global activate flutterfire_cli
```

4. Configure Firebase for this app:

```bash
flutterfire configure
```

This replaces `lib/firebase_options.dart` with real Firebase values and creates the native config files.

5. Publish Firestore rules from `firestore.rules`, or paste them into the Firebase console.

6. Run the app with your OpenAI API key:

```bash
flutter run --dart-define=OPENAI_API_KEY=sk-your-key
```

Optional model override:

```bash
flutter run --dart-define=OPENAI_API_KEY=sk-your-key --dart-define=OPENAI_MODEL=gpt-4o-mini
```

## Firebase Collections

```text
users/{uid}
  name: string
  age: number
  weight: number
  goal: string
  createdAt: timestamp

users/{uid}/workouts/{workoutId}
  goal: string
  timeAvailable: number
  summary: string
  exercises: array
  completed: boolean
  createdAt: timestamp

users/{uid}/progress/{progressId}
  weight: number
  completedWorkouts: number
  createdAt: timestamp
```

## Notes

- The OpenAI key is read from `--dart-define` so it is not committed to source.
- For production, proxy OpenAI requests through a trusted backend or Firebase Cloud Function to avoid exposing API keys in client apps.
- Health and nutrition suggestions should be treated as general guidance, not medical advice.

## If Native Files Need Regeneration

The Android and web scaffolding is included. If your local Flutter version asks to regenerate platform files, run:

```bash
flutter create --project-name fitai --platforms android,ios,web .
```

Keep this project's `lib/`, `pubspec.yaml`, `README.md`, `DEPLOYMENT.md`, `firebase.json`, and `firestore.rules` files.
