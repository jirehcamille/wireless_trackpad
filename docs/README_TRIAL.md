
# Windows Touchpad Configuration Manager
### Trial Software Development for the Wireless Trackpad Project

## Project Overview

The Windows Touchpad Configuration Manager is a trial software project designed to provide users with a centralized interface for customizing their laptop's built-in touchpad settings.

The application will initially be developed and tested using an ASUS VivoBook 15 X507UF running Windows 11 Version 25H2. Its purpose is to demonstrate how a desktop application can communicate with Windows and apply actual changes to the laptop's touchpad settings.

This project serves as the software foundation for the group's main project: an ESP32-based wireless trackpad using a salvaged laptop touchpad.

The trial version will establish the application's interface, configuration controls, and communication architecture before adapting the system to work with the group's own wireless trackpad.

## Objectives

- Develop a Windows-based touchpad configuration application.
- Implement controls that modify actual touchpad settings.
- Explore Windows APIs and system integration.
- Develop a user-friendly configuration interface.
- Establish a reusable frontend and backend architecture.
- Prepare the software for future ESP32 Bluetooth integration.

## Target Device

| Component | Specification |
|---|---|
| Laptop | ASUS VivoBook 15 X507UF |
| Operating System | Windows 11 Version 25H2 |
| Touchpad | ASUS Precision Touchpad |
| Driver Provider | ASUSTeK COMPUTER INC. |
| Driver Version | 16.0.0.11 |

## Features and Scope

The initial version will focus on four touchpad configuration features.

### 1. Pointer Speed
Allows users to adjust the speed of the cursor through a slider.

### 2. Tap-to-Click
Allows users to enable or disable clicking by tapping the touchpad.

### 3. Two-Finger Scrolling
Allows users to enable or disable scrolling using two fingers.

### 4. Scroll Direction
Allows users to switch between natural and traditional scrolling directions.

**Note:** Actual implementation depends on the Windows interfaces and touchpad driver support. Each feature must be verified through testing.

## Technology Stack

### Frontend
- React
- TypeScript
- Vite

Responsibilities:
- Build the configuration manager interface.
- Display touchpad settings.
- Provide sliders, switches, and selection controls.
- Send configuration requests to the backend.
- Display confirmed setting values and operation results.

### Backend
- C#
- .NET

Responsibilities:
- Communicate with Windows system interfaces.
- Read supported touchpad settings.
- Apply configuration changes.
- Validate requests and handle errors.
- Return updated settings to the frontend.

### System Integration
- Windows APIs
- Documented Precision Touchpad configuration interfaces

The application will run locally on Windows. A regular browser application alone cannot directly modify all Windows touchpad settings, so a local Windows integration component will handle system-level operations.

## System Architecture

The trial application will follow this communication flow:

1. The user opens the configuration manager.
2. The user selects or modifies a touchpad setting.
3. The React frontend sends the request to the C#/.NET backend.
4. The backend communicates with the appropriate Windows interface.
5. Windows applies the supported configuration change.
6. The backend returns the operation result.
7. The frontend displays the confirmed setting.

```text
+--------------------------------+
|             USER               |
+--------------------------------+
                |
                v
+--------------------------------+
|    React + TypeScript + Vite   |
|       Configuration UI         |
+--------------------------------+
                |
                v
+--------------------------------+
|          C# / .NET             |
|    Windows Integration Layer  |
+--------------------------------+
                |
                v
+--------------------------------+
|          Windows APIs          |
+--------------------------------+
                |
                v
+--------------------------------+
|    Built-in Laptop Touchpad    |
+--------------------------------+
```

## Application Sections

### Dashboard
- Application overview
- Detected touchpad information
- Current configuration summary

### Touchpad Settings
- Pointer speed
- Tap-to-click
- Two-finger scrolling
- Scroll direction

### Preferences
- Restore default settings
- Application preferences
- About the application
- Version information

## Development Roadmap

| Phase | Task |
|---|---|
| 1 | Research Windows APIs and driver compatibility |
| 2 | Develop the C#/.NET Windows integration component |
| 3 | Develop the React configuration manager interface |
| 4 | Integrate the frontend and backend |
| 5 | Test all four touchpad configuration features |
| 6 | Refine the application and document the results |

## Testing and Validation

The application must be tested against the actual laptop touchpad.

Testing will include:

- Reading the current pointer speed.
- Changing pointer speed and observing cursor behavior.
- Enabling and disabling tap-to-click.
- Enabling and disabling two-finger scrolling.
- Changing scroll direction.
- Verifying whether changes persist after restarting the application.
- Checking error handling and unsupported settings.

## Limitations and Considerations

- Available settings depend on the Windows version, touchpad hardware, and installed driver.
- Not all touchpad settings are necessarily accessible through documented Windows APIs.
- Some operations may require additional permissions.
- The trial implementation is specific to the laptop's built-in touchpad.
- The final wireless trackpad may require a different configuration implementation.

## Connection to the Final Project

This trial project is intended to establish the software foundation for the group's wireless trackpad.

The React interface and general configuration structure will be designed for reuse. When development transitions to the final project, the Windows integration layer will be replaced by an ESP32 Bluetooth communication layer.

| Component | Trial Project | Final Project |
|---|---|---|
| Interface | React + TypeScript | Reused React interface |
| Communication | Local Windows component | Bluetooth Low Energy |
| Device | Built-in laptop touchpad | Salvaged laptop touchpad |
| Controller | Windows touchpad driver | ESP32 |
| Configuration | Windows-supported settings | ESP32-supported settings |

The final implementation will depend on the capabilities of the salvaged touchpad and ESP32 firmware.

## Expected Deliverables

- Working Windows Touchpad Configuration Manager prototype.
- React and TypeScript frontend.
- C#/.NET Windows integration component.
- Tested touchpad configuration controls.
- Documentation of implementation and testing results.
- Reusable software architecture for the final wireless trackpad.

## Project Status

**Status:** Trial development / Prototype

This repository or project directory is intended for the initial Windows-based configuration manager implementation.
