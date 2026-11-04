# GridiFone

**Free and open-source Android app that blocks unwanted calls and SMS — no ads, no sign-up.**

GridiFone is a privacy-focused Android application designed to give users complete control over unwanted calls and SMS messages.

Built with Flutter, Dart, and native Kotlin, GridiFone combines a clean, intuitive interface with Android's native telephony capabilities to provide customizable call and SMS filtering.

No advertisements. No account registration. No unnecessary complexity.

<sub>🚧 **Project status: Prototype — actively under development.**</sub>

## Table of Contents

- [Features](#features)
- [Background](#background)
- [Screenshots](#screenshots)
- [Technology Stack](#technology-stack)
- [Architecture](#architecture)
- [Requirements](#requirements)
- [Installation](#installation)
- [Development](#development)
- [Usage](#usage)
- [Privacy](#privacy)
- [Security](#security)
- [Testing](#testing)
- [CI/CD](#cicd)
- [Contributing](#contributing)
- [License](#license)

## Features

GridiFone is designed around simplicity, privacy, and user control.

### Call and SMS protection

- **Call blocking:** Block unwanted incoming calls using customizable rules.
- **SMS blocking:** Filter unwanted SMS messages independently of calls.
- **Independent filtering:** Configure call and SMS blocking separately for every number.
- **Unknown number protection:** Configure filtering for numbers not included in your trusted contacts.
- **Private number protection:** Configure handling of calls with hidden caller IDs.

### Blocklist management

- **Blocklist:** Maintain a list of numbers you want to block.
- **Allowlist:** Manage trusted numbers that should remain accessible.
- **Contact integration:** Use Android contacts to manage trusted numbers.
- **Individual rules:** Configure call and SMS filtering independently for each entry.

### Activity monitoring

- **Dashboard:** View blocking statistics and protection status.
- **Activity logs:** Review blocked calls and SMS events.
- **Event filtering:** Filter activity by All, Calls, or SMS.
- **Notifications:** Configure notifications for blocked activity.

### Customization

- **Dark AMOLED interface:** Designed with a dark interface and carefully selected accent colors.
- **Theme customization:** Customize the application's appearance.
- **Language settings:** Designed to support localization.
- **CSV export:** Export blocklist data for backup and portability.

### Privacy first

- No advertisements.
- No account registration.
- No mandatory sign-up.
- No unnecessary user profiles.
- Local-first data management.

*Note: Features and native Android integrations are subject to change while the project remains in prototype development.*

## Background

Unwanted calls and SMS messages have become an everyday problem.

Spam calls, telemarketing, fraudulent messages, and unsolicited communications interrupt daily life and can expose users to privacy and security risks.

GridiFone aims to solve this problem through a lightweight, accessible, and privacy-focused Android application.

The project follows three fundamental principles:

1. **Privacy:** Users should not need an account or surrender personal information to manage unwanted communications.
2. **Control:** Users should decide which numbers can reach them and which communication channels should be filtered.
3. **Transparency:** Blocking rules and activity should be understandable, accessible, and manageable directly from the application.

GridiFone is developed as free and open-source software under the MIT License, encouraging transparency, community participation, and independent improvements.

## Screenshots

GridiFone features a dark AMOLED-inspired interface with a bottom navigation bar and four primary sections.

### Home — Overview

The dashboard provides an overview of protection status, blocked activity, and quick actions.

### Blocklist

Manage blocked and allowed phone numbers, search entries, and configure independent call and SMS filtering rules.

### Logs

Review blocking activity and filter events by type:

- All
- Calls
- SMS

### Settings

Configure protection preferences, appearance, notifications, trusted contacts, and blocklist export.

## Technology Stack

GridiFone combines a cross-platform Flutter interface with native Android functionality.

| Component | Technology |
|---|---|
| UI framework | Flutter |
| Programming language | Dart |
| Native Android integration | Kotlin |
| Android build system | Gradle |
| Database | SQLite |
| Flutter database integration | sqflite |
| Native communication | Flutter MethodChannel |
| Android telephony integration | Android Telephony APIs |
| IDE | Visual Studio Code |
| Development OS | Ubuntu 24.04 LTS |
| Static analysis | Dart Analyzer |
| CI/CD | GitHub Actions |

### Android compatibility

| Configuration | Version |
|---|---|
| Minimum SDK | 29 (Android 10) |
| Compile / Target SDK | 35 |
| Platform | Android |

## Architecture

GridiFone follows a layered architecture that separates presentation, data management, and native Android functionality.

### High-level architecture

```text
┌──────────────────────────────────────┐
│           Flutter Application        │
│                                      │
│  ┌────────────┐  ┌────────────────┐  │
│  │ Home       │  │ Blocklist      │  │
│  ├────────────┤  ├────────────────┤  │
│  │ Logs       │  │ Settings       │  │
│  └────────────┘  └────────────────┘  │
│                                      │
│       Presentation / Widgets         │
└──────────────────┬───────────────────┘
                   │
                   ▼
┌──────────────────────────────────────┐
│            Data Layer                │
│                                      │
│  Security Repository                 │
│  Database Service                    │
│  Block Rule Models                   │
│  Blocked Event Models                │
└──────────────┬───────────────┬───────┘
               │               │
               ▼               ▼
┌────────────────────┐  ┌────────────────────┐
│   SQLite Database  │  │ Flutter Method     │
│                    │  │ Channel            │
│ Block Rules        │  └─────────┬──────────┘
│ Blocked Events     │            │
└────────────────────┘            ▼
                      ┌──────────────────────┐
                      │ Native Android       │
                      │ Kotlin Layer         │
                      │                      │
                      │ MainActivity         │
                      │ CallBlockerService   │
                      │ SmsReceiver          │
                      │ MmsReceiver          │
                      │ ContactLookupHelper  │
                      │ AppDatabaseHelper    │
                      └──────────────────────┘
```

### Flutter layer

The Flutter application handles:

- User interface and navigation.
- Blocklist and allowlist management.
- Application settings.
- Activity logs and statistics.
- Local database access.
- Communication with native Android services.

### Native Kotlin layer

The Android implementation handles platform-specific functionality:

- Android telephony role management.
- Native call screening integration.
- SMS delivery handling.
- Contact lookup.
- Native database fallback and event logging.
- Communication with Flutter through MethodChannel.

### Data layer

SQLite provides local persistence for blocking rules and activity events.

The primary data models include:

**BlockRuleModel**

- `number`
- `label`
- `isCallBlocked`
- `isSmsBlocked`

**BlockedEventModel**

- `id`
- `number`
- `eventType`
- `messageBody`
- `timestamp`

The Flutter data layer uses repositories and database services to separate persistence from presentation logic.

## Requirements

### Development environment

- Ubuntu 24.04 LTS (Noble Numbat), or another supported development operating system.
- Flutter SDK.
- Dart SDK (included with Flutter).
- Android SDK.
- Android SDK Platform 35.
- Android SDK Build-Tools.
- Java Development Kit compatible with the configured Gradle and Android Gradle Plugin versions.
- Visual Studio Code.
- Flutter and Dart VS Code extensions.
- A physical Android device or Android emulator.

### Android requirements

- Android 10 (API 29) or newer.
- Required Android permissions and telephony roles.
- Supported Android call-screening capabilities.
- Appropriate system roles and permissions for SMS functionality.

Actual blocking functionality depends on Android's platform restrictions, role requirements, and device implementation.

## Installation

### 1. Clone the repository

```bash
git clone <repository-url>
cd gridifone
```

### 2. Check Flutter installation

```bash
flutter doctor -v
```

Resolve any missing Android SDK, Java, or Flutter dependencies before proceeding.

### 3. Install Flutter dependencies

```bash
flutter pub get
```

### 4. Verify the project

```bash
flutter analyze
```

### 5. Run tests

```bash
flutter test
```

### 6. Run the application

Connect an Android device with USB debugging enabled or start an Android emulator.

```bash
flutter devices
flutter run
```

## Development

### Project structure

```text
gridifone/
├── .github/
│   └── workflows/
│       └── build-and-release.yml
│
├── .gitignore
├── README.md
├── LICENSE
├── analysis_options.yaml
├── pubspec.yaml
│
├── android/
│   ├── app/
│   │   ├── build.gradle
│   │   └── src/main/
│   │       ├── AndroidManifest.xml
│   │       ├── kotlin/
│   │       │   └── com/paratopic/gridifone/
│   │       │       ├── MainActivity.kt
│   │       │       ├── CallBlockerService.kt
│   │       │       ├── SmsReceiver.kt
│   │       │       ├── MmsReceiver.kt
│   │       │       ├── HeadlessSmsSendService.kt
│   │       │       ├── ContactLookupHelper.kt
│   │       │       └── AppDatabaseHelper.kt
│   │       └── res/
│   │
│   ├── gradle/
│   │   └── wrapper/
│   ├── build.gradle
│   └── settings.gradle
│
├── lib/
│   ├── main.dart
│   ├── core/
│   │   ├── constants/
│   │   └── theme/
│   ├── data/
│   │   ├── datasources/
│   │   ├── models/
│   │   └── repositories/
│   ├── presentation/
│   │   ├── screens/
│   │   └── widgets/
│   └── services/
│
└── test/
    ├── unit/
    │   └── block_rules_test.dart
    └── widget/
        └── navigation_test.dart
```

### Code conventions

- Follow Dart and Flutter coding conventions.
- Follow Kotlin coding conventions for native Android components.
- Keep UI components separate from business logic.
- Keep database operations within the data layer.
- Use repositories for data access.
- Keep native Android integration behind the MethodChannel abstraction.
- Document platform-specific behavior.
- Add unit and widget tests for new functionality.

### Useful commands

| Command | Description |
|---|---|
| `flutter pub get` | Install dependencies |
| `flutter analyze` | Run static analysis |
| `flutter test` | Run Flutter tests |
| `flutter clean` | Clean build artifacts |
| `flutter run` | Run on connected device |
| `flutter build apk` | Build Android APK |
| `flutter build appbundle` | Build Android App Bundle |

## Usage

### 1. Launch GridiFone

Open the application and navigate through the four main sections using the bottom navigation bar.

### 2. Configure protection

Use Settings to configure the desired protection preferences and complete any Android system role or permission requests.

### 3. Manage phone numbers

Open Blocklist to add, search, and manage phone numbers.

Choose whether each number should be blocked or allowed, and configure call and SMS filtering independently.

### 4. Review blocking activity

Navigate to Logs to inspect recorded events and filter them by communication type.

### 5. Customize the experience

Use Settings to configure appearance, notifications, trusted contacts, and CSV export.

*Some operations may remain incomplete while the project is in prototype development.*

## Privacy

Privacy is a fundamental design principle of GridiFone.

The project aims to provide essential call and SMS protection without requiring users to create accounts or subscribe to a service.

### Privacy principles

- No advertisements.
- No mandatory account registration.
- Local-first storage.
- Minimal permission requirements.
- No unnecessary collection of personal information.
- Transparent handling of call and SMS data.

### Local data

Blocking rules and activity records are designed to be stored locally using SQLite.

Access to contacts, call-related information, and SMS content is restricted to functionality that requires it.

**Privacy audit:** Actual data handling, backup behavior, network access, logging, and third-party dependencies must be verified before making production privacy guarantees.

## Security

Security and privacy issues are taken seriously.

If you discover a vulnerability, please avoid publishing exploitable details in public issues.

Until a dedicated private reporting channel is established, contact the repository maintainer through an agreed private communication channel.

Security-related contributions should prioritize:

- Secure local data handling.
- Least-privilege Android permissions.
- Safe handling of sensitive SMS content.
- Reliable call and SMS filtering.
- Dependency security.
- Protection against unintended data exposure.

## Testing

GridiFone includes a testing structure for validating application behavior.

### Unit tests

Location: `test/unit/`

Current test coverage includes:

- Block rule validation.
- Contact matching logic.

### Widget tests

Location: `test/widget/`

Current test coverage includes:

- Application navigation.
- Four-tab bottom navigation sanity checks.

### Running tests

```bash
flutter test
```

Static analysis:

```bash
flutter analyze
```

Native Android integration should also be tested on physical devices, particularly call screening, SMS role handling, permissions, and manufacturer-specific behavior.

## CI/CD

GridiFone includes a GitHub Actions workflow:

`.github/workflows/build-and-release.yml`

The workflow is intended to automate:

- Code analysis.
- Automated tests.
- Android APK builds.
- Android App Bundle (AAB) builds.
- GitHub release publishing.

Build and release operations should only be considered production-ready after the workflow has been successfully validated.

## Contributing

Contributions are welcome!

GridiFone is intended to be a community-driven open-source project. Developers, testers, designers, and privacy advocates are encouraged to contribute.

### How to contribute

1. Fork the repository.
2. Create a feature branch.
3. Implement your changes.
4. Run static analysis and tests.
5. Commit your changes.
6. Open a Pull Request.

Example:

```bash
git checkout -b feature/improve-call-filtering

git add .

git commit -m "Improve call filtering"

git push origin feature/improve-call-filtering
```

### Contribution guidelines

- Keep GridiFone free and open-source.
- Do not introduce advertisements.
- Do not introduce mandatory registration.
- Respect user privacy.
- Request only necessary Android permissions.
- Follow existing Flutter and Kotlin conventions.
- Include tests where practical.
- Document new functionality.
- Avoid unnecessary dependencies.
- Consider Android compatibility when modifying native code.

### Reporting bugs

Please open a GitHub Issue and include:

- Android version.
- Device manufacturer and model.
- Steps to reproduce.
- Expected behavior.
- Actual behavior.
- Relevant logs or screenshots.

### Suggesting features

Feature requests are welcome.

Before implementing major architectural changes, consider opening an issue to discuss the proposal.

## License

GridiFone is licensed under the **MIT License**.

You are free to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the software, subject to the terms of the license.

See [LICENSE](LICENSE) for the complete license text.

---

**GridiFone — Take control of your calls and messages.**

Free. Open-source. No ads. No sign-up.

