
# Wireless Trackpad
### ESP32-Based Wireless Trackpad Using a Salvaged Laptop Touchpad

## Project Overview

Wireless Trackpad is a hardware and software development project that aims to convert a salvaged laptop touchpad into a wireless input device using an ESP32 microcontroller.

The project focuses on developing a functional wireless trackpad that can connect to a Windows computer through Bluetooth. It will support basic touchpad operations and provide battery-level reporting through Bluetooth.

A dedicated Windows configuration manager will also be developed to allow users to view device information and customize the supported trackpad settings and gestures.

The project combines embedded systems development, wireless communication, hardware interfacing, and desktop application development.

## Objectives

- Repurpose a salvaged laptop touchpad into a wireless input device.
- Use an ESP32 microcontroller to process touchpad input.
- Establish wireless communication between the trackpad and a Windows computer.
- Implement basic pointer, clicking, and scrolling functionality.
- Provide battery-level information through Bluetooth.
- Develop a Windows configuration manager for device settings.
- Explore customizable multi-finger gestures, depending on hardware capabilities.

## Project Scope and Features

### 1. Basic Trackpad Functionality

The wireless trackpad is intended to support:

- Cursor movement
- Left-click
- Right-click
- Double-click
- Drag and drop
- Basic scrolling

These functions should work after the device is paired and connected to a compatible Windows computer, without requiring the configuration manager to be open.

### 2. Bluetooth Connectivity

The ESP32 will handle wireless communication between the physical trackpad and the Windows computer.

Intended functionality:

- Bluetooth pairing
- Device connection and disconnection
- Reconnection behavior
- Wireless pointer input
- Battery-level reporting

The exact Bluetooth implementation will depend on the selected ESP32 board and its supported Bluetooth capabilities.

### 3. Battery Monitoring

Battery monitoring is part of the basic device functionality.

The system is intended to:

- Measure the battery level.
- Report battery percentage through Bluetooth.
- Make battery information available to compatible Windows interfaces.
- Provide low-battery indications.
- Support battery status display in the configuration manager.

The proposed implementation will investigate the standard BLE Battery Service (UUID 0x180F) and Battery Level characteristic (UUID 0x2A19).

**Note:** Actual battery display behavior in Windows must be verified with the selected ESP32 implementation and target Windows version. Reporting a battery percentage through BLE does not guarantee that Windows will display it in every system interface.

### 4. Configuration Manager

A dedicated Windows application will be developed to manage the wireless trackpad.

Proposed features:

- Device connection status
- Battery percentage
- Pointer sensitivity
- Clicking settings
- Scrolling settings
- Supported multi-finger gestures
- Customizable gesture actions
- Restore default settings
- Device information

The configuration manager will be optional for basic trackpad operation. Its purpose is to provide additional configuration and device management features.

### 5. Multi-Finger Gestures

The project aims to explore customizable multi-finger gestures.

Possible examples include:

- Three-finger swipe down to take a screenshot.
- Three-finger swipe up to open Task View.
- Three-finger swipe left or right to switch applications.
- Other user-defined gesture actions.

The availability of these features depends on whether the salvaged touchpad provides accessible multi-touch data, including finger coordinates and contact information.

## Proposed System Architecture

The intended system will consist of the following components:

1. Salvaged laptop touchpad
2. ESP32 microcontroller
3. Battery and power management circuit
4. Bluetooth communication
5. Windows computer
6. Optional Windows configuration manager

```text
+--------------------------------+
|      SALVAGED LAPTOP           |
|          TOUCHPAD              |
+--------------------------------+
                |
                v
+--------------------------------+
|        ESP32 MICROCONTROLLER   |
|                                |
| - Touchpad data processing     |
| - Gesture processing           |
| - Bluetooth communication      |
| - Battery monitoring           |
+--------------------------------+
                |
                v
+--------------------------------+
|         BLUETOOTH              |
|                                |
| - HID input                    |
| - Battery reporting            |
| - Configuration communication  |
+--------------------------------+
                |
                v
+--------------------------------+
|        WINDOWS COMPUTER        |
|                                |
| - Cursor movement              |
| - Clicking and scrolling       |
| - Battery information          |
+--------------------------------+
                |
                v
+--------------------------------+
|    CONFIGURATION MANAGER       |
|       (OPTIONAL)               |
|                                |
| - Device status                |
| - Battery percentage           |
| - Trackpad settings            |
| - Gesture customization        |
+--------------------------------+
```

## Proposed Hardware Components

The final hardware configuration will depend on the salvaged touchpad and the hardware team's testing.

| Component | Purpose |
|---|---|
| Salvaged laptop touchpad | Main touch input surface |
| ESP32 development board | Main microcontroller |
| Battery | Powers the wireless device |
| Battery monitoring circuit or fuel gauge | Measures battery level |
| Charging and protection circuit | Handles battery charging and protection |
| Voltage regulation components | Provides the required operating voltage |
| Connecting wires and connectors | Hardware interfacing |
| Enclosure | Houses and protects the components |

**Important:** The touchpad's exact pinout, voltage requirements, and communication protocol must be identified before connecting it to the ESP32. The hardware team must verify whether the touchpad uses I2C, SPI, USB, SMBus, or another interface.

## Proposed Software and Technologies

### ESP32 Firmware
- C++
- Arduino Framework or ESP-IDF
- Bluetooth HID
- BLE GATT services
- Battery monitoring
- Touchpad data processing

### Windows Configuration Manager
- React
- TypeScript
- Vite
- Bluetooth Low Energy communication through Web Bluetooth or another suitable Windows integration method

### Optional Windows Integration
A native Windows companion component may be considered if background notifications or Windows-specific functionality cannot be handled reliably through the browser-based manager.

## Configuration Manager Architecture

The final configuration manager is intended to communicate directly with the ESP32 through Bluetooth Low Energy.

```text
+--------------------------------+
|     REACT CONFIGURATION UI     |
|                                |
| - Dashboard                    |
| - Trackpad Settings            |
| - Gesture Customization        |
| - Preferences                  |
+--------------------------------+
                |
                v
+--------------------------------+
|      BLE COMMUNICATION LAYER   |
|                                |
| - Connect to ESP32             |
| - Read device information      |
| - Read battery level           |
| - Send configuration requests  |
+--------------------------------+
                |
                v
+--------------------------------+
|        ESP32 FIRMWARE          |
|                                |
| - Receive settings             |
| - Validate configuration       |
| - Save settings                 |
| - Apply supported changes      |
+--------------------------------+
                |
                v
+--------------------------------+
|        WIRELESS TRACKPAD       |
+--------------------------------+
```

The ESP32 should store configuration values in non-volatile storage so that user preferences can remain available after the configuration manager is closed or the device is restarted.

## Wi-Fi and Bluetooth

The selected ESP32 board may support both Wi-Fi and Bluetooth.

Bluetooth will be the primary communication method for:

- Wireless pointer input
- Device connection
- Battery reporting
- Configuration communication

Wi-Fi may be reserved for optional future features, such as local network communication, firmware updates, or a web-based interface.

Wi-Fi will not be required for basic wireless trackpad operation.

Simultaneous Wi-Fi and Bluetooth operation must be tested on the selected ESP32 board because both may share radio resources.

## Development Roadmap

### Phase 1: Hardware Identification and Research
- Identify the salvaged touchpad model and controller.
- Determine its pinout and operating voltage.
- Identify its communication protocol.
- Verify whether multi-touch data is accessible.
- Select the ESP32 development board.
- Determine the battery and power requirements.

### Phase 2: Touchpad and ESP32 Integration
- Connect the touchpad to the ESP32.
- Establish communication between the components.
- Read and interpret touchpad input.
- Test pointer movement and basic input functions.

### Phase 3: Bluetooth Implementation
- Implement Bluetooth HID functionality.
- Establish pairing and connection with Windows.
- Test cursor movement, clicking, and scrolling.
- Investigate BLE Battery Service integration.
- Test battery-level reporting.

### Phase 4: Configuration Manager Development
- Develop the Windows application interface.
- Implement BLE communication.
- Display device information and battery percentage.
- Implement supported configuration controls.
- Test saving and applying settings.

### Phase 5: Gesture Development
- Investigate available multi-touch data.
- Implement supported gesture recognition.
- Develop customizable gesture mappings.
- Test gesture actions on Windows.

### Phase 6: Integration and Testing
- Integrate hardware and software.
- Test wireless performance.
- Test battery reporting and power consumption.
- Verify connection and reconnection behavior.
- Test configuration persistence.
- Refine the overall device and application.

## Hardware Team Coordination

The hardware team must provide the following information to support firmware and configuration manager development:

### Touchpad Information
- Exact touchpad model or part number
- Front and back photographs
- Connector type and pin count
- Pinout documentation
- Operating voltage
- Communication protocol
- Initialization requirements
- Available sample code or documentation

### Multi-Touch Capabilities
- Maximum supported number of fingers
- Whether individual finger coordinates are accessible
- Whether contact IDs are provided
- Whether pressure or contact information is available
- Whether raw or processed touch data can be read

### ESP32 Information
- Exact ESP32 board or module
- Bluetooth capabilities
- Available GPIO pins
- Supported BLE HID implementation
- Ability to support HID and configuration GATT services
- Wi-Fi and Bluetooth coexistence considerations

### Battery and Power Information
- Battery type and capacity
- Operating voltage
- Charging circuit
- Battery protection
- Battery monitoring method
- Charging status detection
- Expected operating time

## Important Technical Considerations

### Touchpad Compatibility
Not all salvaged laptop touchpads use the same communication protocol. The exact controller and pinout must be identified before firmware development.

### Multi-Touch Support
Custom gestures require access to sufficient multi-touch information. If the touchpad only provides basic processed pointer input, advanced gesture customization may be limited.

### Bluetooth HID and BLE GATT
The device must support wireless input and battery/configuration communication. The selected ESP32 and Bluetooth stack must be tested for compatibility with the intended services.

### Battery Reporting
A battery monitoring circuit or fuel gauge may be needed to obtain reliable battery percentage readings. Windows battery display behavior must also be tested.

### Configuration Persistence
User settings should be saved on the ESP32 so that the device retains its configuration after disconnection or restart.

### Windows Compatibility
The final device is intended for Windows computers. Its HID behavior, battery reporting, and configuration manager communication must be tested on the target Windows environment.

## Expected Deliverables

- Functional ESP32-based wireless trackpad prototype.
- Salvaged laptop touchpad integrated with the ESP32.
- Bluetooth HID input functionality.
- Battery monitoring and BLE battery reporting.
- Windows configuration manager.
- Supported customizable trackpad settings.
- Multi-finger gesture functionality, subject to hardware capability.
- Hardware and software documentation.
- Testing and evaluation results.

## Project Status

**Status:** Hardware and software development / Prototype planning

The final hardware configuration, touchpad communication protocol, and supported features will be confirmed through hardware testing.

## Relationship Between the Trial and Final Projects

The Windows Touchpad Configuration Manager trial is the initial software development stage of this project.

The trial uses the laptop's built-in touchpad and Windows integration to establish the application interface and configuration architecture.

The final implementation will reuse the general interface while replacing the Windows integration layer with Bluetooth communication to the ESP32.

The objective is to develop a dedicated Windows application that can manage and customize the group's own wireless trackpad.
