# AutoReply Pro 📱💬

*Personal Android Auto-Reply Application for SMS & Calls*

[![Android](https://img.shields.io/badge/Platform-Android-green.svg)](https://android.com)
[![Kotlin](https://img.shields.io/badge/Language-Kotlin-blue.svg)](https://kotlinlang.org)
[![API](https://img.shields.io/badge/API-21%2B-brightgreen.svg)](https://android-arsenal.com/api?level=21)

## 🌟 Overview

AutoReply Pro is a custom Android application designed to automatically respond to incoming SMS messages and missed calls with customizable messages. Built specifically for professional use with reliable automated communication responses.

### ✨ Key Features

- **🚀 Instant Auto-Reply**: Automatic responses to SMS and missed calls
- **🏖️ Vacation Mode**: Special responder for existing contacts during vacation
- **🔒 One-Time Reply Logic**: Prevents spam - replies only once per contact
- **⚙️ Customizable Messages**: Personalized auto-reply templates
- **📊 Contact Management**: Track and manage replied contacts
- **🔔 Foreground Service**: Reliable background operation
- **🛡️ Permission Management**: Secure and compliant permission handling

## 📋 Table of Contents

- [Features](#-key-features)
- [Installation](#-installation)
- [Usage](#-usage)
- [Configuration](#-configuration)
- [Technical Details](#-technical-details)
- [Support](#-support)

## 🚀 Installation

### Prerequisites
- Android device running API 21+ (Android 5.0+)
- SMS and Phone permissions
- Notification access permission

### Build from Source
```bash
git clone https://github.com/tharinduxd0/AutoReply-Pro.git
cd AutoReply-Pro
./gradlew assembleDebug
```

## 💡 Usage

### Quick Start Guide

1. **Launch the app** and grant required permissions
2. **Toggle the main switch** to enable auto-reply functionality
3. **Customize messages** in Settings for SMS and missed calls
4. **Start the service** for reliable background operation

### Core Functionality

#### 📨 SMS Auto-Reply
- Automatically responds to new SMS messages
- One-time reply per contact (prevents spam)
- Customizable reply message
- Smart contact detection

#### 📞 Missed Call Auto-Reply
- Detects missed calls automatically
- Sends SMS reply to missed call numbers
- Separate customizable message for calls
- Integrated with SMS blocking system

#### 🏖️ Vacation Mode
- Special mode for temporary auto-replies
- Works with existing contacts who already received replies
- Separate vacation message
- Session-based management

## ⚙️ Configuration

### Message Templates

Navigate to **Settings** to customize your auto-reply messages:

#### SMS Reply Template
```
Default: "Thank you for texting me. Visit my website!"
```

#### Missed Call Reply Template
```
Default: "Sorry, I missed your call. Please visit my website!"
```

#### Vacation Message Template
```
Default: "Thanks for texting! I'm currently on vacation but will get back to you soon."
```

### Advanced Settings

- **Toggle Auto-Reply**: Master switch for all auto-reply features
- **Vacation Mode**: Temporary responder for existing contacts
- **Service Management**: Control background service operation
- **Contact Management**: View and manage replied contacts

## 🔧 Technical Details

### Architecture Overview
```
┌─────────────────┐    ┌──────────────────┐    ┌─────────────────┐
│   MainActivity  │────│  SmsReceiver     │────│  SmsUtil        │
│                 │    │                  │    │                 │
│ ┌─────────────┐ │    │ ┌──────────────┐ │    │ ┌─────────────┐ │
│ │ UI Controls │ │    │ │ SMS Handler  │ │    │ │ Send Logic  │ │
│ │ Settings    │ │    │ │ Vacation     │ │    │ │ Retry Logic │ │
│ │ Toggles     │ │    │ │ Logic        │ │    │ │ Error Handle│ │
│ └─────────────┘ │    │ └──────────────┘ │    │ └─────────────┘ │
└─────────────────┘    └──────────────────┘    └─────────────────┘
         │                       │                       │
         │              ┌──────────────────┐              │
         └──────────────│ CallStateListener│──────────────┘
                        │                  │
                        │ ┌──────────────┐ │
                        │ │ Call Handler │ │
                        │ │ Missed Calls │ │
                        │ └──────────────┘ │
                        └──────────────────┘
```

### Key Components

- **SmsReceiver**: Handles incoming SMS messages with race condition protection
- **CallStateListener**: Monitors call states for missed call detection
- **VacationResponderUtils**: Manages vacation mode functionality
- **PhoneNumberUtils**: Normalizes and manages phone number variations
- **MyForegroundService**: Ensures reliable background operation

### Performance Optimizations

- **Asynchronous Processing**: Non-blocking SMS handling
- **Race Condition Prevention**: Thread-safe contact management
- **Memory Efficient**: Optimized SharedPreferences usage
- **Battery Friendly**: Efficient background service implementation

## 🚨 Important Notice - Missed Call Functionality

### Understanding Android Limitations

**SMS Auto-Reply** ✅ Works automatically in background
- Android natively supports background SMS handling
- No additional service required
- Replies work immediately after enabling main toggle

**Missed Call Auto-Reply** ⚠️ Requires manual service start
- Android **DOES NOT** support 24/7 call monitoring in background
- **You MUST manually start the foreground service**
- Without foreground service = **NO missed call replies**

### How to Enable Missed Call Auto-Reply

1. Open the app
2. Enable the main auto-reply toggle
3. **Click "Start Service" button** (This is mandatory!)
4. You should see a persistent notification
5. Now missed calls will be detected and replied to

> **🔑 Key Point**: If you want missed call auto-replies to work, the foreground service must be running. SMS works without it, but calls absolutely need it due to Android's background limitations.

### Required Permissions

```xml
<uses-permission android:name="android.permission.RECEIVE_SMS" />
<uses-permission android:name="android.permission.SEND_SMS" />
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
<uses-permission android:name="android.permission.POST_NOTIFICATIONS" />
<uses-permission android:name="android.permission.READ_CALL_LOG" />
<uses-permission android:name="android.permission.FOREGROUND_SERVICE" />
```

## 🛠️ Development Stack

### Built With
- **Kotlin** - Primary programming language
- **Android SDK** - Android development framework
- **SharedPreferences** - Data persistence
- **Coroutines** - Asynchronous programming
- **Material Design** - UI components

### Project Structure
```
src/main/java/com/tharinduxd/autoreplyapp/
├── MainActivity.kt              # Main app interface
├── SmsReceiver.kt              # SMS handling logic
├── CallStateListener.kt        # Call state monitoring
├── VacationResponderUtils.kt   # Vacation mode management
├── PhoneNumberUtils.kt         # Phone number utilities
├── SmsUtil.kt                  # SMS sending utilities
├── MyForegroundService.kt      # Background service
├── SettingsActivity.kt         # Settings configuration
└── ManageNumbersActivity.kt    # Contact management
```

## 📞 Support

### Need Help?
For any questions, issues, or technical support:

**Developer**: [tharinduxd](https://github.com/tharinduxd0)  
**LinkedIn Post**: [AutoReply Pro on LinkedIn](https://www.linkedin.com/posts/tharinduxd_productivity-androidapp-autoreply-activity-7363831824105529346-A3Uq)


### Common Issues

#### App Not Responding to SMS
- Check if all required permissions are granted
- Verify the main toggle is enabled
- Restart the foreground service

#### Delayed Replies
- Ensure the app is not battery optimized
- Verify foreground service is running

#### Vacation Mode Not Working
- Confirm vacation mode toggle is enabled
- Check if contacts are in the eligible list
- Verify vacation message is configured

## 📸 Screenshot

![AutoReply Pro Screenshot](https://i.postimg.cc/4NgqsxD9/Screenshot-2025-08-20-132655.png)

---

<div align="center">

**Built for Professional Auto-Reply Solutions**

*project by [tharinduxd](https://github.com/tharinduxd0)*

</div>
