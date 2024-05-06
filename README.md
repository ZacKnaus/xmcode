# XMCode: Extended Machine Code

XMCode (Extended Machine Code) is a next-generation machine control format designed to provide a flexible and extensible way to configure and control various types of machines, including CNC machines, 3D printers, laser cutters, and robotic arms. It aims to address the limitations of traditional G-code and offer a more structured and readable format for machine control.

## Overview

XMCode consists of two main components:

1. **Settings JSON**: A comprehensive machine configuration file that defines the machine's capabilities, limitations, and settings. It includes information about axes, tooling, sensors, custom commands, and various machine-specific parameters.

2. **XMCode JSON**: A machine control file that contains the actual commands and parameters for controlling the machine. It uses a human-readable format and supports advanced features like parameter validation and asynchronous command execution.

The goal of XMCode is to provide a standardized and extensible format that can be easily adapted to different machines and use cases. It aims to simplify the process of configuring and controlling machines, while also enabling more advanced functionality and flexibility compared to traditional G-code.

## Notable Highlights

XMCode offers several notable highlights that extend the functionality beyond traditional G-code:

1. **Comprehensive Machine Configuration**: XMCode provides a comprehensive machine configuration file (`settings.json`) that allows you to define the machine's capabilities, limitations, and settings in a structured and readable format. This includes information about axes, tooling, sensors, custom commands, and various machine-specific parameters, enabling more advanced and flexible machine control.

2. **Tooling Management**: XMCode supports a wide range of tooling options, including spindles, lasers, 3D printers, automatic tool changers, vacuum systems, cooling systems, and lubrication systems. Each tooling type has its own set of configurable parameters and commands, allowing for precise control and customization based on the specific requirements of the machine and its application.

3. **Sensor Integration**: XMCode enables seamless integration of various sensors, such as limit switches, temperature sensors, color sensors, torque sensors, current sensors, encoders, load cells, strain gauges, and back EMF sensors. These sensors can be easily configured in the `settings.json` file, specifying their type, interface, response frequency, and trigger actions. This allows for real-time monitoring, feedback, and automated responses based on sensor data.

4. **Custom Commands**: XMCode allows you to define custom commands that are not specific to any tooling. These custom commands can be easily configured in the `settings.json` file, specifying the function to be executed, required parameters, and whether the command should be executed asynchronously. This extensibility enables you to implement machine-specific functionality and integrate with external systems or custom software.

5. **Asynchronous Command Execution**: XMCode supports asynchronous command execution, allowing certain commands to be executed in the background without blocking the main motion control loop. This is particularly useful for commands that involve longer processing times or external interactions, such as tool changing, vacuum control, or lubrication systems. Asynchronous execution ensures smooth and responsive machine operation.

6. **Time Synchronization**: XMCode introduces time synchronization capabilities, enabling precise timing and coordination of machine operations. Each line of XMCode can include a time synchronization block, specifying the start time and the time distance from the start of execution. This feature is particularly useful for applications that require precise timing, such as synchronized multi-axis motion or coordination with external devices.

7. **Security and Encryption**: XMCode prioritizes security by providing options for secure communication and encrypted XMCode. The `settings.json` file allows you to configure security settings, such as the security mode (secure or encrypted) and the encryption algorithm used. This ensures that sensitive machine data and commands are protected from unauthorized access or tampering.

8. **Monitoring and Feedback**: XMCode supports monitoring capabilities through the integration of webcams and other monitoring devices. The `settings.json` file allows you to configure monitoring devices, specifying their type, resolution, frame rate, connection type, and control commands. This enables real-time monitoring, remote access, and visual feedback during machine operation.

9. **Extensibility and Customization**: XMCode is designed with extensibility and customization in mind. The `settings.json` file provides a flexible and modular structure that allows you to easily add new features, tooling types, sensors, or custom commands. This extensibility ensures that XMCode can adapt to the evolving needs of machine control and accommodate future advancements in technology.

10. **Human-Readable Format**: XMCode uses a human-readable JSON format for both the `settings.json` and `xmcode.json` files. This makes it easier for users to understand, modify, and troubleshoot machine configurations and control commands. The structured format also facilitates version control, collaboration, and automation in machine control workflows.

These notable highlights demonstrate how XMCode extends the functionality of traditional G-code, providing a more advanced, flexible, and user-friendly approach to machine control. By leveraging the capabilities of XMCode, users can unlock new possibilities in machining, robotics, and automation.

## Settings JSON

The `settings.json` file is responsible for defining the machine's configuration and capabilities. It includes the following main sections:

### 1. Axes

The `axes` section defines the properties and settings for each axis of the machine. It includes the following sub-sections:

- `name`: The unique name of the axis.
- `alias`: A user-friendly alias for the axis (e.g., "x", "y", "z").
- `motor_type`: The type of motor used for the axis (e.g., "stepper", "servo").
- `drive_type`: The type of drive mechanism used for the axis (e.g., "leadscrew", "belt").
- `gearbox`: The associated gearbox for the axis.
- `range_of_motion`: The minimum and maximum limits for the axis movement.
- `soft_limits`: The soft limits for the axis, used to restrict movement within a safer range.
- `homing_direction`: The direction of homing movement for the axis.
- `homing_speed`: The speed at which homing is performed for the axis.
- `limit_switches`: The properties of limit switches for the axis, including aliases and trigger actions.
- `comments`: Additional comments or notes about the axis.
- `maintenance`: Maintenance-related information for the axis, such as lubrication and calibration intervals.

### 2. Disallowed Coordinates

The `disallowed_coordinates` section defines a list of coordinate ranges that are not allowed for movement. This can be used to prevent the machine from moving into certain areas or colliding with obstacles.

### 3. Tooling

The `tooling` section specifies the available tools and their associated settings. It includes sub-sections for different types of tools, such as:

- `spindle`: Settings for the spindle, including maximum RPM, horsepower, tool offsets, wear compensation, and commands.
- `laser`: Settings for the laser, including maximum power, wavelength, tool offsets, and commands.
- `3d_printer`: Settings for the 3D printer, including maximum temperature, nozzle diameter, filament diameter, bed leveling, and commands.
- `atc`: Settings for the automatic tool changer, including the number of slots, tool identification, tool change time, and commands.
- `vacuum`: Settings for the vacuum system, including maximum pressure, flow rate, hose diameter, and commands.
- `cooling`: Settings for the cooling system, including coolant type, tank capacity, pump flow rate, and commands.
- `lubrication`: Settings for the lubrication system, including lubricant type, viscosity, reservoir capacity, and commands.

### 4. Sensors

The `sensors` section defines the available sensors and their configurations. Each sensor is identified by a unique alias and includes the following properties:

- `type`: The type of sensor (e.g., "limit_switch", "temperature", "color_sensor").
- `interface`: The communication interface used by the sensor (e.g., "digital", "analog", "i2c").
- `pin` or `address`: The pin or address to which the sensor is connected.
- `response_frequency`: The frequency at which the sensor provides updates or can be read.
- `last_content`: The last data provided by the sensor.
- `last_triggered`: The timestamp of the last trigger event.
- `interpreter_function`: The function used to interpret the sensor's raw values into meaningful data.
- `trigger_actions`: The actions to be performed when certain conditions are met based on the sensor's interpreted data.

### 5. Motor Control Boards

The `motor_control_boards` section defines the motor control boards used in the machine and their configurations. Each board is identified by a unique name and includes the following properties:

- `type`: The type of motor control board (e.g., "stepper_driver", "servo_driver", "multi_driver").
- `model`: The specific model or identifier of the board.
- `interface`: The communication interface used by the board (e.g., "uart", "pwm", "spi").
- `address`: The address of the board, if applicable.
- `max_current`: The maximum current supported by the board.
- `microstep_resolution`: The microstep resolution of the board (for stepper drivers).
- `step_angle`: The step angle of the motors connected to the board (for stepper drivers).
- `protocol`: The communication protocol used by the board (e.g., "marlin", "grbl", "klipper").
- `axes`: The list of axes controlled by the board.

### 6. Custom Commands

The `custom_commands` section allows defining custom commands that are not specific to any tooling. Each custom command includes the following properties:

- `function`: The function to be executed when the command is called.
- `parameters`: The parameters required for the command, including their types and ranges.
- `async`: Indicates whether the command should be executed asynchronously.
- `comments`: Additional comments or notes about the custom command.

### 7. Power-on Setup

The `power_on_setup` section defines the initial setup routine when the machine is powered on. It includes the following properties:

- `enabled`: Indicates whether the power-on setup routine is enabled or disabled.
- `homing_sequence`: Specifies the order in which axes should be homed during the power-on setup.

### 8. Monitoring

The `monitoring` section defines the monitoring capabilities of the machine, such as webcams. Each monitoring device includes the following properties:

- `type`: The type of monitoring device (e.g., "webcam").
- `resolution`: The resolution of the monitoring device.
- `frame_rate`: The frame rate of the monitoring device.
- `connection_type`: The type of connection used by the monitoring device (e.g., "usb", "network").
- `device_id` or `ip_address`: The device ID or IP address of the monitoring device.
- `commands`: The available commands for controlling the monitoring device.

### 9. Security

The `security` section defines the security settings for XMCode. It includes the following properties:

- `xmcode_security`: The security mode and algorithm used for encrypting or securing XMCode.

### 10. Synchronization

The `synchronization` section defines the time synchronization settings for XMCode. It includes the following properties:

- `time_synchronization`: Indicates whether time synchronization is enabled, the start time, and the time format used.

### 11. User

The `user` section includes user-specific settings, such as the timezone.

## Attributes

The `attributes` section in the `settings.json` file provides additional information about the machine's physical characteristics and capabilities. It includes sub-sections for:

- `machine`: Overall attributes of the machine, such as accuracy and repeatability.
- `axes`: Attributes specific to each axis, such as maximum speed, acceleration, steps per mm, and backlash compensation.
- `tooling`: Attributes specific to each tooling, such as spindle power, laser focus diameter, and 3D printer nozzle size.
- `gearboxes`: Attributes specific to each gearbox, such as type, ratio, maximum torque, and efficiency.

## XMCode JSON

The `xmcode.json` file contains the actual commands and parameters for controlling the machine. It follows a structured format and includes sections for axes movement, tooling commands, custom commands, and synchronization.

The detailed structure and usage of the `xmcode.json` file will be covered in a separate section of the documentation.

## Conclusion

XMCode provides a comprehensive and flexible format for configuring and controlling various types of machines. By defining the machine's capabilities, limitations, and settings in the `settings.json` file, and using the `xmcode.json` file for actual machine control, XMCode enables advanced functionality, extensibility, and ease of use compared to traditional G-code.

For more detailed information on each section and property of the `settings.json` and `xmcode.json` files, please refer to the respective documentation sections.
