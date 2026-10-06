# Acadence

## Project overview
Acadence is an integrated research-support mobile app for postgraduate students and their consultants. It centralises discovery, document management, secure collaboration, progress tracking and personalised research recommendations into a single mobile-first experience with offline capabilities and biometric log in. The purpose of this application is to reduce redundancy in the postgraduate research lifecycle by providing one app that supports resource discovery, draft iteration, consultant feedback and networking.

## Key Goals 
- For Students: The app allows students to access recommended resources, organize drafts, receive consultant feedback, and track their progress on a single platform. It also includes an article viewing and saving feature and empowers students to post their own articles to recieve peer feedback.
- For Consultants: Consultants use the platform to guide students through personalized feedback, resource suggestions, and progress monitoring.
- Usability: The application features a clean and simplistic interface with a professional aesthetic using a calming palette of blue, white, and grey to enhance usability and reinforce Acadence’s unique branding

## Core Features
- Role-based authentication: Student and Consultant
- SSO with Google
- Biometric unlock (FaceID and/or Fingerprint) for supported devices
- Offline mode using Room DB with two-way sync to Firestore
- Document upload and resource library
- Consultant feedback threads with ratings and read receipts
- Realtime chat 
- Push notifications for deadlines, feedback and announcements (Firebase Cloud Messaging)
- AI assistant brainstorming help, draft review prompts, personalised resource recommendations
- Article "For You" feed and save-for-offline reading
- Multilanguage support: English and Afrikaans
- Settings page: profile, language, notification preferences, biometric toggle
- Accessibility-focused UI: clear contrast palette, consistent navigation

## Design considerations
#### User roles and security
- Role-based access control: different UI and API privileges for Student and Consultant
- Authentication model: OAuth/JWT token-based SSO; optional biometric unlocking on device
- Transport & storage: TLS for all network transport; encrypted local storage for sensitive data

#### Offline-first UX
- Local cache with Room as primary store for offline interactions (draft edits, messages)
- Two-way sync strategy: local writes queued and reconciled with Firestore when online
- Conflict policy: last-write-wins for low-risk data; versioned documents for critical content

#### Scalability & modularity
- Serverless backend (Firebase Cloud Functions) to scale event-driven workloads
- Firestore collections partitioned by tenant/user; Cloud Storage for large artifacts
- Clear separation of concerns: Authentication, Document Service, Collaboration, AI layer

#### Privacy & compliance
- Minimal personal data in public areas; opt-in sharing for profile visibility
- Audit trails for document changes and feedback

#### Accessibility & localisation
- Simple layouts, high-contrast colour palette (blue/white/grey), support for multiple languages
- Usability-first navigation with consistent patterns across student/consultant flows

## DevOps Practices & CI/CD Implementation

### Continuous Integration (CI)
- Source Control: All code maintained in GitHub for version control and collaboration  
- Automated Builds: Each commit triggers builds and unit tests  
- Static Code Analysis: GitHub Actions linters + Android Studio linters detect issues early  
- Testing: Automated unit and integration tests prevent regressions  

### Continuous Deployment (CD)
- Staging Environment: Successfully tested builds deployed automatically for UAT  
- Approval Gate: QA lead approval promotes builds to production  
- Rollback Mechanism: Version-controlled releases allow quick reverts  

### Deployment Workflow
1. Code Commit → push to GitHub  
2. Build & Test → CI pipeline compiles and runs tests  
3. Containerization → Docker image created and stored in Google Cloud Artifact Registry  
4. Staging Deployment → deployed for automated/manual testing  
5. Production Deployment → auto-deployed after approval  
6. Monitoring & Logging → Firebase App Check + cloud monitoring track performance  
7. Scaling & Backup → Auto-scaling policies + scheduled backups ensure reliability  

This workflow ensures reliable, rapid, and secure deployment while enabling the team to respond efficiently to bugs, scaling requirements, and system updates.

## Release notes

version 1

- Initial prototype: authentication flow, UI mockups, basic navigation and wireframes, project planning and UML artifacts.

version 2 — Final Project

#### Summary 
This release marks the final project submission and implements the full suite of planned features, including the major innovations described below. The app is production-ready for demonstration and evaluation.

#### Implemented features in this release

- AI Assistant: Integrated AI assistant for brainstorming, draft review suggestions, and personalised resource recommendations in the For You feed.
- Biometric Authentication: Device-level biometric quick-unlock (FaceID and Fingerprint) for faster secure access.
- Offline Mode: Offline-first architecture using Room DB with background sync to Firestore for drafts, saved articles, and messages.
- Single Sign-On (SSO): SSO with Google for streamlined account access and role claims.
- Settings Page: Full settings UI allowing users to change language (English / Afrikaans), biometric toggle, and account settings. 
- Real-time Notifications: Push notifications via Firebase Cloud Messaging for new messages, feedback, admin announcements, and deadlines.
- Multilanguage Support: English and Afrikaans interfaces and translations across primary user flows.
- Document Management: File upload & metadata, version tracking and consultant assignment workflow with review threads.
- Real-time Collaboration: Realtime chat, feedback threads, read receipts and in-chat file sharing.
- Security & Data Protection: TLS transport, Firestore rules skeleton, local encrypted storage for sensitive data.
- CI Pipeline: GitHub Actions for build verification, unit testing and linting; deploy jobs scaffolded for Firebase.

#### Notes
- AI assistant is delivered as an MVP with server-side endpoints for recommendations and draft analysis. Future work will expand accuracy and ranking.
- End-to-end encrypted messaging is planned for v1.x but is not included in this release.
- Play Store packaging steps are included, but final store submission may require additional assets and signing keys. 

#### Changelog (high-level)
Added: AI assistant, biometric unlock, offline sync, SSO, settings, realtime notifications, Afrikaans support, admin console, document versioning, messaging enhancements

## Tech Stack

| Component       | Technology                                      |
|-----------------|------------------------------------------------|
| Language        | Kotlin                                         |
| IDE             | Android Studio                                 |
| Database        | Firebase Firestore                             |
| Authentication  | Firebase Authentication (SSO + Biometrics)     |
| File Storage    | Firebase Storage                               |
| Notifications   | Firebase Cloud Messaging                        |
| Target SDK      | API 36 (Android 14)                            |

## Setup

1. Clone the repository
2. Add your Firebase google-services.json file under /app.
3. Enable Firebase Authentication, Firestore, and Cloud Storage.
4. Run on a physical device or emulator (API 36+).

## Development & Version Control
Repository hosted on GitHub with feature-based commits
GitHub Actions used for build verification and CI
Code structured for scalability and maintainability

## Team Members
- Nail Arslan — API, backend & testing
- Tyrus Fernandes — backend logic, scheduling
- Oratile Kodisang — UI design, UX polishing
- Basetsana Mokgoatsana — front-end and accessibility
- Refentse de Jenga — documentation 
