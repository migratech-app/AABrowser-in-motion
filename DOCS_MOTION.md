# Android Auto/Automotive - Motion Restrictions Documentation

This document explains the current implementation and available options to enable the application to run while the vehicle is in motion.

## Current Configuration (v1.6+)

The application has been optimized to bypass typical "greyed out" or "blocked" states in Android Auto and Android Automotive.

### 1. Manifest Optimization
- **App Category**: Changed from `game` to `productivity`. This is critical as the `game` category is automatically blocked by the system during driving.
- **Distraction Optimized Flags**: All user-facing activities are now tagged with `<meta-data android:name="distractionOptimized" android:value="true" />`.
- **Hardware Acceleration**: Enabled for smooth rendering of web content.

### 2. Automotive Features (`automotive_app_desc.xml`)
- Added `<uses name="template" />` in addition to `<uses name="media" />` to signal more flexible capability to the system.

## Available Testing Options

A new **Experimental / Testing** section has been added to the application's internal Settings menu.

- **Bypass motion restrictions (Experimental)**: A persistent toggle to signal the app to remain active even if it detects motion. Note: System-level blocks (from Android Auto or the car manufacturer) may still apply if they don't honor the `distractionOptimized` flag.
- **Motion Status Capability**: Shows the current "Distraction Optimized" status in the settings UI.

## Troubleshooting "Greyed Out" Icon in Android Auto

If the application icon is still greyed out or won't start in Android Auto:

1. **Check Developer Mode**: In the Android Auto settings on your phone, ensure "Developer mode" is enabled and "Unknown sources" is checked.
2. **App Category Enforcement**: Some head units strictly enforce the `appCategory`. If `productivity` is still blocked, it may be necessary to test with `maps` or `navigation`.
3. **Manifest Conflicts**: Ensure that no other component in the app is missing the `distractionOptimized` flag.
4. **Phone-Side Restrictions**: Some phone manufacturers (e.g., Samsung, Huawei) have their own motion-sensing restrictions that might override the Android Auto settings.

## Future Research & Development

- **Dynamic Capability Reporting**: Investigating if we can report different capabilities based on the car's current `CarUxRestrictions`.
- **Car Library Integration**: Deeper integration with `androidx.car.app` could provide more robust ways to handle driving state changes.
