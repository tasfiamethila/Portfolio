# ClubNest

ClubNest is a Java-based Android application for smart university club management. It includes:

- role-based authentication for Admin, Club Executive, and Student
- club, notice, membership, and event management
- approval workflows for executives, memberships, and event registrations
- profile management, in-app notifications, and export support

## Firebase-ready backend

This project is now Firebase-ready.

By default:

- if Firebase is **not configured**, the app falls back to the built-in local demo mode
- if Firebase **is configured**, authentication and app data move to Firebase Auth + Cloud Firestore

Firebase file location:

- [app/google-services.json](/C:/Users/MS/Documents/Codex/2026-04-23-android-app-name-clubnest-smart-university/app/google-services.json)

### What moves to Firebase

- User authentication: Firebase Authentication
- Users, clubs, notices, events, approvals, membership requests, registrations, notifications: Cloud Firestore
- Storage dependency is already added for future file upload support such as payment screenshots and club logos

### How to connect your own Firebase project

1. Create a Firebase project.
2. Add an Android app with package name `com.clubnest.app`.
3. Enable `Email/Password` sign-in in Firebase Authentication.
4. Create a Cloud Firestore database.
5. Download `google-services.json` from Firebase Project Settings.
6. Put the file inside the `app/` folder as `app/google-services.json`.
7. Publish Firestore rules from [firebase/firestore.rules](/C:/Users/MS/Documents/Codex/2026-04-23-android-app-name-clubnest-smart-university/firebase/firestore.rules)
8. Optionally publish Storage rules from [firebase/storage.rules](/C:/Users/MS/Documents/Codex/2026-04-23-android-app-name-clubnest-smart-university/firebase/storage.rules)
9. Rebuild the app.

If `google-services.json` is missing, the project stays in local demo mode.

### Admin setup in Firebase mode

- Admin is still **not** created from public sign up
- create a normal account first
- then edit that user's Firestore document in `users/{uid}` and set:
  - `role = "ADMIN"`
  - `status = "ACTIVE"`
  - `executiveApprovalStatus = "APPROVED"`
  - `emailVerified = true` if needed

### Important note about mobile login

- Email login works immediately with Firebase Auth
- Mobile-number login in this starter resolves the user's email from Firestore first
- if your Firestore rules block unauthenticated access to user lookup, sign in with email instead
- for production-grade phone login, add Firebase Phone Auth or a dedicated secure lookup flow

## Demo mode

When Firebase is not configured, you can still use the app in local demo mode.

Demo admin credentials in local demo mode:

- Email: `admin@clubnest.edu`
- Password: `Admin@123`

Notes:

- Firebase mode uses real email verification and password reset emails.
- Local demo mode uses SharedPreferences-backed sample data and demo OTP-style fallback flow.
