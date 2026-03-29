# mittManager-Mobile-App (React Native Complete Setup Guide) 🚀

## Part 1: System Requirements Check

### Windows Users:
- Windows 10 or 11 (64-bit)
- 8GB RAM minimum (16GB recommended)
- 20GB free disk space

### Mac Users:
- macOS Monterey or later
- 8GB RAM minimum (16GB recommended)
- 20GB free disk space
- **Mac required for iOS development**

### Linux Users:
- Ubuntu 18.04+ or similar
- 8GB RAM minimum

---

## Part 2: Install Required Software

### Step 1: Install Node.js & npm

**Windows/Mac:**
```bash
# Download from: https://nodejs.org/
# Choose LTS version (e.g., 18.x or 20.x)
# Run installer with default settings

# Verify installation
node --version  # Should show v18.x.x or higher
npm --version   # Should show 9.x.x or higher
```

**Linux (Ubuntu/Debian):**
```bash
# Install Node.js 20.x
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt-get install -y nodejs

# Verify
node --version
npm --version
```

### Step 2: Install Java Development Kit (JDK) - For Android

**Windows:**
```bash
# Download JDK 11 or 17 from:
# https://adoptium.net/

# Install and note the installation path
# Example: C:\Program Files\Eclipse Adoptium\jdk-11.0.20.8-hotspot\
```

**Mac:**
```bash
# Using Homebrew (install Homebrew first if needed)
brew install --cask zulu11

# Verify
java -version
```

**Linux:**
```bash
sudo apt-get install openjdk-11-jdk

# Verify
java -version
```

### Step 3: Install Android Studio - For Android

**All Platforms:**

1. **Download Android Studio:**
   - https://developer.android.com/studio
   - Download & install (takes 10-15 minutes)

2. **First Launch Setup:**
   ```
   - Open Android Studio
   - Click "More Actions" > "SDK Manager"
   ```

3. **Install Required Components:**
   ```
   SDK Platforms Tab:
   ✓ Android 13.0 (Tiramisu) - API Level 33
   ✓ Android 12.0 (S) - API Level 31
   
   SDK Tools Tab:
   ✓ Android SDK Build-Tools
   ✓ Android Emulator
   ✓ Android SDK Platform-Tools
   ✓ Intel x86 Emulator Accelerator (HAXM) - Windows only
   ✓ Google Play services
   ```

4. **Set Environment Variables:**

**Windows:**
```bash
# Open Environment Variables:
# Win + X > System > Advanced system settings > Environment Variables

# Add New System Variables:
Variable: ANDROID_HOME
Value: C:\Users\YOUR_USERNAME\AppData\Local\Android\Sdk

Variable: JAVA_HOME
Value: C:\Program Files\Eclipse Adoptium\jdk-11.0.20.8-hotspot

# Edit Path variable, add:
%ANDROID_HOME%\platform-tools
%ANDROID_HOME%\emulator
%ANDROID_HOME%\tools
%ANDROID_HOME%\tools\bin
```

**Mac/Linux (.zshrc or .bashrc):**
```bash
# Open terminal and edit:
nano ~/.zshrc  # or ~/.bashrc for bash

# Add these lines:
export ANDROID_HOME=$HOME/Library/Android/sdk
export PATH=$PATH:$ANDROID_HOME/emulator
export PATH=$PATH:$ANDROID_HOME/platform-tools
export PATH=$PATH:$ANDROID_HOME/tools
export PATH=$PATH:$ANDROID_HOME/tools/bin

# Save (Ctrl+O, Enter, Ctrl+X)
# Reload:
source ~/.zshrc
```

**Verify Android Setup:**
```bash
# Close and reopen terminal
adb --version  # Should show Android Debug Bridge version
```

### Step 4: Install Xcode - For iOS (Mac Only)

```bash
# 1. Open App Store
# 2. Search "Xcode"
# 3. Install (10-12 GB, takes time)

# 4. After installation:
sudo xcode-select --switch /Applications/Xcode.app/Contents/Developer
sudo xcodebuild -runFirstLaunch

# 5. Install Command Line Tools:
xcode-select --install

# 6. Install CocoaPods:
sudo gem install cocoapods

# Verify:
pod --version
```

---

## Part 3: Create Your First React Native Project

### Method 1: React Native CLI (Traditional)

```bash
# Install React Native CLI globally
npm install -g react-native-cli

# Create new project
npx react-native init MittiManager

# Navigate to project
cd MittiManager

# Project structure created:
MittiManager/
├── android/          # Android native code
├── ios/             # iOS native code
├── node_modules/    # Dependencies
├── App.tsx          # Main app file
├── package.json     # Dependencies list
└── ...
```

### Method 2: Expo (Recommended for Beginners)

```bash
# Create Expo app
npx create-expo-app MittiManager

# Navigate to project
cd MittiManager

# Install dependencies
npm install

# Project structure:
MittiManager/
├── App.js           # Main app file
├── package.json     # Dependencies
├── app.json         # Expo config
└── ...
```

---

## Part 4: Setup Android Emulator

### Create Virtual Device:

```bash
# 1. Open Android Studio
# 2. Click "More Actions" > "Virtual Device Manager"
# 3. Click "Create Device"
# 4. Select "Pixel 5" or "Pixel 6" > Next
# 5. Download "Tiramisu" (API 33) system image > Next
# 6. Name: "MittiManager_Emulator" > Finish

# Start emulator from command line:
emulator -avd MittiManager_Emulator
```

---

## Part 5: Run Your App

### For React Native CLI:

**Android:**
```bash
# Terminal 1 - Start Metro bundler:
npx react-native start

# Terminal 2 - Run Android:
npx react-native run-android

# If emulator not running, start it first:
emulator -avd MittiManager_Emulator
```

**iOS (Mac only):**
```bash
# Install iOS dependencies:
cd ios
pod install
cd ..

# Terminal 1 - Start Metro:
npx react-native start

# Terminal 2 - Run iOS:
npx react-native run-ios
```

### For Expo:

```bash
# Start development server:
npx expo start

# Press 'a' for Android emulator
# Press 'i' for iOS simulator (Mac only)
# Scan QR code with Expo Go app on phone
```

---

## Part 6: Install Required Packages for Mitti Manager

```bash
# Navigation
npm install @react-navigation/native
npm install @react-navigation/native-stack
npm install react-native-screens react-native-safe-area-context

# Storage (localStorage replacement)
npm install @react-native-async-storage/async-storage

# Icons
npm install react-native-vector-icons

# For Expo, use:
npx expo install react-native-screens react-native-safe-area-context
npx expo install @react-native-async-storage/async-storage
```

---

## Part 7: Test Your Setup

### Create a Simple Test App:

**Edit App.js or App.tsx:**

```javascript
import React from 'react';
import {
  SafeAreaView,
  View,
  Text,
  StyleSheet,
  TouchableOpacity,
} from 'react-native';

export default function App() {
  return (
    <SafeAreaView style={styles.container}>
      <View style={styles.content}>
        <Text style={styles.title}>🚜 मिट्टी Manager</Text>
        <Text style={styles.subtitle}>React Native Setup Complete!</Text>
        
        <TouchableOpacity style={styles.button}>
          <Text style={styles.buttonText}>Get Started →</Text>
        </TouchableOpacity>
      </View>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#0D1117',
  },
  content: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    padding: 20,
  },
  title: {
    fontSize: 32,
    fontWeight: '900',
    color: '#E6EDF3',
    marginBottom: 10,
  },
  subtitle: {
    fontSize: 16,
    color: '#8B949E',
    marginBottom: 40,
  },
  button: {
    backgroundColor: '#F0A500',
    paddingHorizontal: 30,
    paddingVertical: 15,
    borderRadius: 14,
  },
  buttonText: {
    color: '#000',
    fontSize: 16,
    fontWeight: '700',
  },
});
```

**Run it:**
```bash
# React Native CLI:
npx react-native run-android  # or run-ios

# Expo:
npx expo start
```

---

## Part 8: Common Issues & Solutions

### Issue 1: "adb not found"
```bash
# Windows: Restart computer after setting environment variables
# Mac/Linux: Run source ~/.zshrc or source ~/.bashrc
```

### Issue 2: Metro bundler port already in use
```bash
npx react-native start --reset-cache --port 8082
```

### Issue 3: Android build fails
```bash
cd android
./gradlew clean
cd ..
npx react-native run-android
```

### Issue 4: iOS CocoaPods error (Mac)
```bash
cd ios
pod deintegrate
pod install
cd ..
```

### Issue 5: "Command not found: npx"
```bash
# Reinstall Node.js from nodejs.org
# Make sure to select "Add to PATH" during installation
```

---

## Part 9: Development Tools

### VS Code Extensions (Recommended):

```
1. React Native Tools (Microsoft)
2. ES7+ React/Redux/React-Native snippets
3. Prettier - Code formatter
4. React-Native/React/Redux snippets
5. Auto Import
```

### Chrome DevTools:
```bash
# Press Ctrl+M (Android) or Cmd+M (iOS) in emulator
# Select "Debug" > Opens Chrome DevTools
```

---

## Part 10: Next Steps Checklist

✅ Node.js installed & verified
✅ JDK installed (Android)
✅ Android Studio setup complete
✅ Xcode installed (Mac, for iOS)
✅ Environment variables configured
✅ Emulator/Simulator working
✅ First app runs successfully
✅ Required packages installed

---

## 🎯 Quick Command Reference

```bash
# Create new project
npx react-native init AppName

# Start Metro bundler
npx react-native start

# Run on Android
npx react-native run-android

# Run on iOS
npx react-native run-ios

# Clear cache
npx react-native start --reset-cache

# Check React Native info
npx react-native info
```

---

Kya aap chahte ho main ab:
1. **Mitti Manager app ka complete React Native code** banau?
2. **Expo version** setup karoon (easier)?
3. Kisi specific step mein help chahiye?

Bataiye kahan se shuru karein! 💪
