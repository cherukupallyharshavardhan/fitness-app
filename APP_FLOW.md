# How FitAI Works

1. The user signs up with email and password.
2. Firebase Auth creates the account.
3. The app stores the profile in Firestore under `users/{uid}`.
4. The Home screen listens to Firestore and shows the user's goal, latest workout, calories, and completed workouts.
5. When the user taps Generate Plan, the app sends the user's goal and available time to OpenAI.
6. OpenAI returns structured workout JSON with exercises, sets, reps, and notes.
7. The generated workout is saved in `users/{uid}/workouts`.
8. The Diet screen can analyze a meal and estimate calories, macros, and next meal suggestion.
9. The Diet screen can also generate a full daily diet plan from the user's goal, weight, and food preference.
10. The Chat screen keeps an in-memory ChatGPT-style conversation and sends fitness questions to OpenAI.
11. The Profile screen saves weight entries and completed workout totals in `users/{uid}/progress`.
12. If the logged-in user's profile has `role: user`, FitAI opens the customer layout.
13. If the logged-in user's profile has `role: admin`, FitAI opens the separate admin layout.
14. The admin layout has Dashboard, Users, and Controls screens.
15. Admin Controls can enable or disable Workout AI, Diet AI, Chat Coach, and maintenance mode.

## Runtime Services

- `AuthService`: Firebase email/password authentication.
- `FirestoreService`: user profile, workouts, and progress CRUD.
- `OpenAIService`: workout generation, diet analysis, and chat responses.
- `AppState`: Provider state that connects UI screens to services.

## Deploy Targets

- Android APK: `flutter build apk --release --dart-define=OPENAI_API_KEY=sk-your-key`
- Android Play Store bundle: `flutter build appbundle --release --dart-define=OPENAI_API_KEY=sk-your-key`
- Firebase Hosting web build: `flutter build web --release --dart-define=OPENAI_API_KEY=sk-your-key`
