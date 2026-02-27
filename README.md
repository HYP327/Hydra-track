HydraTrack — Daily Hydration Tracker

> **Shake. Drink. Thrive.** — A smart hydration tracking Android app built with Kotlin that uses your phone's accelerometer to log water intake with a simple shake gesture.

---
 📖 Table of Contents

- [About the Project](#about-the-project)
- [Problem Statement](#problem-statement)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Sensor Usage](#sensor-usage)
- [App Screens](#app-screens)
- [Data Collection](#data-collection)
- [Admin Dashboard & Excel Export](#admin-dashboard--excel-export)
- [Getting Started](#getting-started)
- [Installation](#installation)
- [Project Structure](#project-structure)
- [Requirements](#requirements)
- [License](#license)



## 📌 About the Project

**HydraTrack** is an Android mobile application developed in **Kotlin** as part of an academic project. The app addresses a common health challenge — people forgetting to drink enough water throughout the day — by offering a fun, gesture-based way to log hydration using the phone's built-in **accelerometer sensor**.

Every time the user drinks a glass of water, they simply **shake their phone** and the app automatically logs 250ml. The app tracks progress toward a personalized daily goal, sends smart reminders, and visualizes hydration trends over time.

For developers and researchers, the app collects anonymous usage data from registered users, which can be viewed through a separate **Admin Dashboard** and exported to a structured **Excel (.xlsx) file** for analysis.



 🚨 Problem Statement

Dehydration is one of the most common and overlooked health issues. Most people do not drink the recommended 2–3 liters of water per day, often simply because they forget. Existing hydration apps require too many manual taps or are overly complex. 

**HydraTrack** solves this by making water logging as effortless as possible — just shake your phone. Combined with smart reminders and visual progress tracking, the app builds a sustainable hydration habit without friction.

 ✨ Features

 👤 User Features
- **Shake-to-Log** — Shake the phone to instantly log 250ml of water intake using the accelerometer
- **Manual Logging** — Tap the "+ Add Glass" button as a backup option
- **Personalized Daily Goal** — Set a custom hydration goal based on your age and weight
- **Progress Dashboard** — Real-time water progress bar showing current vs. target intake
- **Push Notifications & Reminders** — Smart reminders at customizable intervals (every 1h, 2h, etc.)
- **History & Charts** — 7-day bar chart and weekly trend line chart to visualize hydration habits
- **Dark Mode** — Full dark theme support for comfortable use at night
- **User Profile** — Store personal data (name, age, weight, daily goal)

### 🛠️ Developer / Admin Features
- **Admin Dashboard** — Separate web-based panel showing all registered users and their activity logs
- **Excel Export** — One-click export of all user data to a clean `.xlsx` file using Apache POI
- **Device Analytics** — Tracks device model, app sessions, reminder response rate, and more

---

 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Language | Kotlin |
| UI Framework | Jetpack Compose |
| Sensor API | Android SensorManager (Accelerometer) |
| Local Database | Room (SQLite) |
| Charts | MPAndroidChart |
| Notifications | WorkManager + NotificationManager |
| Excel Export | Apache POI (`poi-ooxml`) |
| Admin Dashboard | HTML / JavaScript |
| Build System | Gradle |
| Min SDK | Android 8.0 (API 26) |
| Target SDK | Android 14 (API 34) |

---

 📡 Sensor Usage

HydraTrack uses the device's built-in **Accelerometer** (`TYPE_ACCELEROMETER`) to detect shake gestures.

### How it works:
1. The app registers a listener on the accelerometer sensor when the home screen is active.
2. The sensor continuously reads the force applied on the X, Y, and Z axes.
3. When the combined acceleration force exceeds a defined threshold (subtracting Earth's gravity), the app recognizes it as a **shake event**.
4. A cooldown period prevents multiple logs from a single shake.

```kotlin
// Core shake detection logic
val acceleration = sqrt(x * x + y * y + z * z) - SensorManager.GRAVITY_EARTH
if (acceleration > SHAKE_THRESHOLD) {
    logWaterIntake(250) // Log 250ml
}
```

This approach requires **no internet**, no external hardware, and works entirely on-device.

---

 📱 App Screens

| Screen | Description |
|---|---|
| 🌊 Splash Screen | Animated intro, routes to Onboarding or Home |
| 📝 Onboarding | First-launch profile setup (name, age, weight, goal) |
| 🏠 Home Screen | Water progress bar, shake prompt, daily summary |
| 📊 History Screen | 7-day bar chart + weekly trend line chart |
| ⚙️ Settings Screen | Goal adjustment, reminder frequency, dark mode toggle |

---

## 📊 Data Collection

The app collects the following data per user for developer analytics:

| Field | Description | Example |
|---|---|---|
| `user_id` | Unique user identifier | UUID-8f3a... |
| `name` | User's first name | John |
| `age` | User's age | 22 |
| `weight_kg` | User's weight in kilograms | 70 |
| `daily_goal_ml` | Personalized hydration goal | 2000 |
| `date` | Log date | 2026-02-26 |
| `total_intake_ml` | Total water logged that day | 1750 |
| `goal_achieved` | Whether the goal was met | No |
| `shake_count` | Number of shake events logged | 7 |
| `reminders_sent` | Push notifications sent that day | 4 |
| `sessions_count` | Number of app opens | 3 |
| `device_model` | User's device model | Samsung Galaxy A54 |

> ⚠️ All data is stored locally on the device. No data is sent to external servers without explicit consent.

---

 🖥️ Admin Dashboard & Excel Export

The **Admin Dashboard** is a separate lightweight interface (HTML/JS or Kotlin Desktop) designed for developers to:

- View a table of all registered app users
- Browse daily hydration logs per user
- Filter data by date range or user
- Export all data to a structured **Excel (.xlsx)** file with a single click

### Excel Export Sample Output

| User ID | Name | Age | Weight | Goal (ml) | Intake (ml) | Goal Met | Shakes | Date |
|---|---|---|---|---|---|---|---|---|
| UUID-001 | John | 22 | 70kg | 2000 | 1750 | No | 7 | 2026-02-26 |
| UUID-002 | Maria | 25 | 58kg | 1800 | 1800 | Yes | 8 | 2026-02-26 |

The export is powered by **Apache POI**, generating a properly formatted `.xlsx` file ready for analysis in Microsoft Excel, Google Sheets, or any spreadsheet tool.

---

 🚀 Getting Started

### Prerequisites
- Android Studio (Hedgehog or later)
- Kotlin 1.9+
- Android device or emulator with API 26+
- JDK 17

```bash
git clone https://github.com/your-username/HydraTrack.git
cd HydraTrack
```

 Open in Android Studio
1. Open **Android Studio**
2. Click **"Open an Existing Project"**
3. Select the cloned `HydraTrack` folder
4. Let Gradle sync complete
5. Run the app on a device or emulator

---

 📲 Installation

 Install via APK (End Users)
1. Download the latest `.apk` from the [Releases](https://github.com/your-username/HydraTrack/releases) section
2. On your Android phone, go to **Settings → Security → Enable "Install from Unknown Sources"**
3. Open the downloaded `.apk` file and tap **Install**
4. Launch **HydraTrack** and complete the onboarding

 Build from Source (Developers)
```bash
./gradlew assembleDebug
# APK will be at: app/build/outputs/apk/debug/app-debug.apk
```

---

 📁 Project Structure

```
HydraTrack/
├── app/
│   ├── src/main/
│   │   ├── java/com/hydratrack/
│   │   │   ├── ui/
│   │   │   │   ├── SplashScreen.kt
│   │   │   │   ├── OnboardingScreen.kt
│   │   │   │   ├── HomeScreen.kt
│   │   │   │   ├── HistoryScreen.kt
│   │   │   │   └── SettingsScreen.kt
│   │   │   ├── sensor/
│   │   │   │   └── ShakeDetector.kt
│   │   │   ├── data/
│   │   │   │   ├── UserProfile.kt
│   │   │   │   ├── WaterLog.kt
│   │   │   │   ├── AppDatabase.kt
│   │   │   │   └── HydraRepository.kt
│   │   │   ├── notifications/
│   │   │   │   └── ReminderManager.kt
│   │   │   └── utils/
│   │   │       └── Constants.kt
│   │   └── res/
├── admin-dashboard/
│   ├── index.html
│   ├── dashboard.js
│   └── ExcelExporter.kt
├── build.gradle
└── README.md
```
---

 👨‍💻 Author
Abissi Nsimo & Chipidje Miyo
 📄 License
This project is developed for academic purposes.  
© 2026 HydraTrack. All rights reserved.

> 💡 *"You are not tired. You are dehydrated. Shake it up!"*
