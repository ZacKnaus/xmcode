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

2. **Tooling Management**: XMCode supports a wide range of tooling options, such as spindles, lasers, 3D printers, automatic tool changers, vacuum systems, cooling systems, and lubrication systems. Each tooling type has its own set of configurable parameters and commands, allowing for precise control and customization based on the specific requirements of the machine and its application.

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
  - Stepper motors are commonly used for precise positioning and are controlled by providing step and direction signals.
  - Servo motors are used for applications requiring continuous rotation and are controlled using PWM signals.
- `drive_type`: The type of drive mechanism used for the axis (e.g., "leadscrew", "belt", "rack_and_pinion").
  - Leadscrew drives convert rotary motion into linear motion using a threaded rod and a nut.
  - Belt drives use a toothed belt and pulleys to transmit motion between the motor and the axis.
  - Rack and pinion drives use a geared rack and a pinion to convert rotary motion into linear motion.
- `gearbox`: The associated gearbox for the axis, which is defined in the `gearboxes` section of the `attributes`.
  - Gearboxes are used to change the speed, torque, or direction of the motor's output.
  - The `gearbox` property specifies the name of the gearbox configuration to be used for the axis.
- `range_of_motion`: The minimum and maximum limits for the axis movement.
  - `min`: The minimum position of the axis in its unit of measurement (e.g., millimeters, degrees).
  - `max`: The maximum position of the axis in its unit of measurement.
  - `enabled`: A boolean value indicating whether the range of motion limits are enabled or disabled.
- `soft_limits`: The soft limits for the axis, used to restrict movement within a safer range.
  - `min`: The minimum soft limit position of the axis.
  - `max`: The maximum soft limit position of the axis.
  - `enabled`: A boolean value indicating whether the soft limits are enabled or disabled.
- `homing_direction`: The direction of homing movement for the axis (e.g., "min", "max").
  - Homing is the process of moving the axis to a known reference position.
  - The `homing_direction` specifies whether the axis should move towards the minimum or maximum position during homing.
- `homing_speed`: The speed at which homing is performed for the axis, typically specified in the unit of measurement per second (e.g., mm/s, degrees/s).
- `limit_switches`: The properties of limit switches for the axis.
  - `min`: The alias of the minimum limit switch sensor defined in the `sensors` section.
  - `max`: The alias of the maximum limit switch sensor defined in the `sensors` section.
- `comments`: Additional comments or notes about the axis.
- `maintenance`: Maintenance-related information for the axis.
  - `lubrication`: Lubrication maintenance settings.
    - `maintenance_interval_days`: The interval in days between lubrication maintenance tasks.
    - `last_performed`: The date and time when the last lubrication maintenance was performed.
    - `next_due`: The date and time when the next lubrication maintenance is due.
  - `calibration`: Calibration maintenance settings.
    - `maintenance_interval_days`: The interval in days between calibration maintenance tasks.
    - `last_performed`: The date and time when the last calibration maintenance was performed.
    - `next_due`: The date and time when the next calibration maintenance is due.

### 2. Disallowed Coordinates

The `disallowed_coordinates` section defines a list of coordinate ranges that are not allowed for movement. This can be used to prevent the machine from moving into certain areas or colliding with obstacles.

- Each entry in the `disallowed_coordinates` list represents a range of coordinates that are not allowed.
  - `min`: The minimum value of the disallowed coordinate range.
  - `max`: The maximum value of the disallowed coordinate range.

### 3. Tooling

The `tooling` section specifies the available tools and their associated settings. It includes sub-sections for different types of tools, such as:

- `spindle`: Settings for the spindle, which is a rotating tool used for cutting or drilling.
  - `max_rpm`: The maximum rotational speed of the spindle in revolutions per minute (RPM).
  - `hp`: The horsepower rating of the spindle motor.
  - `tool_offsets`: The offset values for each tool associated with the spindle.
    - Each tool offset is specified using the tool name as the key and the offset values in the x, y, and z axes.
  - `wear_compensation`: The wear compensation values for the spindle in the x, y, and z axes.
  - `commands`: The available commands for the spindle.
    - `on`: The command to turn on the spindle.
      - `function`: The name of the function to be executed when the command is called.
      - `comments`: Additional comments or notes about the command.
    - `off`: The command to turn off the spindle.
      - `function`: The name of the function to be executed when the command is called.
      - `comments`: Additional comments or notes about the command.
    - `adjust_speed`: The command to adjust the speed of the spindle.
      - `function`: The name of the function to be executed when the command is called.
      - `parameters`: The parameters required for the command.
        - `rpm`: The rotational speed parameter.
          - `type`: The data type of the parameter (e.g., "number").
          - `min`: The minimum allowed value for the parameter.
          - `max`: The maximum allowed value for the parameter.
      - `async`: A boolean value indicating whether the command should be executed asynchronously.
      - `comments`: Additional comments or notes about the command.
- `laser`: Settings for the laser tool, which is used for cutting or engraving.
  - `max_power`: The maximum power output of the laser in watts.
  - `wavelength`: The wavelength of the laser in nanometers.
  - `tool_offsets`: The offset values for each tool associated with the laser.
    - Each tool offset is specified using the tool name as the key and the offset values in the x, y, and z axes.
  - `commands`: The available commands for the laser.
    - `on`: The command to turn on the laser.
      - `function`: The name of the function to be executed when the command is called.
      - `comments`: Additional comments or notes about the command.
    - `off`: The command to turn off the laser.
      - `function`: The name of the function to be executed when the command is called.
      - `comments`: Additional comments or notes about the command.
    - `set_power`: The command to set the power of the laser.
      - `function`: The name of the function to be executed when the command is called.
      - `parameters`: The parameters required for the command.
        - `power`: The laser power parameter.
          - `type`: The data type of the parameter (e.g., "number").
          - `min`: The minimum allowed value for the parameter.
          - `max`: The maximum allowed value for the parameter.
      - `async`: A boolean value indicating whether the command should be executed asynchronously.
      - `comments`: Additional comments or notes about the command.
- `3d_printer`: Settings for the 3D printer tool, which is used for additive manufacturing.
  - `max_temp`: The maximum temperature that the 3D printer can reach in degrees Celsius.
  - `nozzle_diameter`: The range of supported nozzle diameters for the 3D printer.
    - `min`: The minimum nozzle diameter in millimeters.
    - `max`: The maximum nozzle diameter in millimeters.
  - `filament_diameter`: The diameter of the filament used by the 3D printer in millimeters.
  - `bed_leveling`: Settings related to bed leveling for the 3D printer.
    - `enabled`: A boolean value indicating whether bed leveling is enabled or disabled.
    - `grid_size`: The size of the grid used for bed leveling.
      - `x`: The number of grid points in the x-axis.
      - `y`: The number of grid points in the y-axis.
    - `last_leveled`: The timestamp of the last bed leveling process.
    - `command`: The custom command for performing bed leveling.
      - `function`: The name of the function to be executed for bed leveling.
  - `commands`: The available commands for the 3D printer.
    - `extrude`: The command to extrude filament.
      - `function`: The name of the function to be executed when the command is called.
      - `parameters`: The parameters required for the command.
        - `length`: The length of filament to extrude.
          - `type`: The data type of the parameter (e.g., "number").
          - `min`: The minimum allowed value for the parameter.
          - `max`: The maximum allowed value for the parameter.
      - `async`: A boolean value indicating whether the command should be executed asynchronously.
      - `comments`: Additional comments or notes about the command.
    - `retract`: The command to retract filament.
      - `function`: The name of the function to be executed when the command is called.
      - `parameters`: The parameters required for the command.
        - `length`: The length of filament to retract.
          - `type`: The data type of the parameter (e.g., "number").
          - `min`: The minimum allowed value for the parameter.
          - `max`: The maximum allowed value for the parameter.
      - `async`: A boolean value indicating whether the command should be executed asynchronously.
      - `comments`: Additional comments or notes about the command.
    - `set_temp`: The command to set the temperature of the nozzle.
      - `function`: The name of the function to be executed when the command is called.
      - `parameters`: The parameters required for the command.
        - `temp`: The temperature parameter.
          - `type`: The data type of the parameter (e.g., "number").
          - `min`: The minimum allowed value for the parameter.
          - `max`: The maximum allowed value for the parameter.
      - `async`: A boolean value indicating whether the command should be executed asynchronously.
      - `comments`: Additional comments or notes about the command.

The `tooling` section provides a flexible and extensible way to define various types of tools and their associated settings. The examples shown above, such as spindle, laser, and 3D printer, are just a few possibilities. You can add more tooling types and customize their settings based on your specific machine and application requirements.

### 4. Sensors

The `sensors` section defines the available sensors and their configurations. Each sensor is identified by a unique alias and includes the following properties:

- `type`: The type of sensor (e.g., "limit_switch", "temperature", "color_sensor", "torque_sensor", "current_sensor", "encoder", "load_cell", "strain_gauge", "back_emf_sensor").
- `interface`: The communication interface used by the sensor (e.g., "digital", "analog", "i2c", "spi").
- `pin` or `address`: The pin number or address to which the sensor is connected, depending on the interface.
- `response_frequency`: The frequency at which the sensor provides updates or can be read, typically specified in Hz.
- `last_content`: The last data provided by the sensor.
- `last_triggered`: The timestamp of the last trigger event.
- `interpreter_function`: The name of the function used to interpret the sensor's raw values into meaningful data.
- `trigger_actions`: The actions to be performed when certain conditions are met based on the sensor's interpreted data.
  - `condition`: The condition that triggers the action (e.g., a specific value or range).
  - `function`: The name of the function to be executed when the condition is met.
  - `async`: A boolean value indicating whether the action should be executed asynchronously.

### 5. Motor Control Boards

The `motor_control_boards` section defines the motor control boards used in the machine and their configurations. Each board is identified by a unique name and includes the following properties:

- `type`: The type of motor control board (e.g., "stepper_driver", "servo_driver", "multi_driver").
- `model`: The specific model or identifier of the board (e.g., "TMC2209", "L298N", "custom_board").
- `interface`: The communication interface used by the board (e.g., "uart", "pwm", "spi", "i2c").
- `address`: The address of the board, if applicable (e.g., "0x00", "0x01").
- `max_current`: The maximum current supported by the board, typically specified in amps.
- `microstep_resolution`: The microstep resolution of the board, which determines the precision of the stepper motor movement (e.g., 256, 128, 64).
- `step_angle`: The step angle of the motors connected to the board, specified in degrees (e.g., 1.8, 0.9).
- `protocol`: The communication protocol used by the board (e.g., "marlin", "grbl", "klipper").
- `axes`: The list of axes controlled by the board, referencing the axis names defined in the `axes` section.

### 6. Custom Commands

The `custom_commands` section allows defining custom commands that are not specific to any tooling. Each custom command includes the following properties:

- `function`: The name of the function to be executed when the command is called.
- `parameters`: The parameters required for the command, if any.
 - Each parameter is defined as a key-value pair, with the parameter name as the key and its properties as the value.
   - `type`: The data type of the parameter (e.g., "number", "string", "boolean").
   - `min`: The minimum allowed value for the parameter, if applicable.
   - `max`: The maximum allowed value for the parameter, if applicable.
- `async`: A boolean value indicating whether the command should be executed asynchronously.
- `comments`: Additional comments or notes about the custom command.

### 7. Power-on Setup

The `power_on_setup` section defines the initial setup routine when the machine is powered on. It includes the following properties:

- `enabled`: A boolean value indicating whether the power-on setup routine is enabled or disabled.
- `homing_sequence`: An array specifying the order in which axes should be homed during the power-on setup, referencing the axis names defined in the `axes` section.

### 8. Monitoring

The `monitoring` section defines the monitoring capabilities of the machine, such as webcams. Each monitoring device includes the following properties:

- `type`: The type of monitoring device (e.g., "webcam").
- `resolution`: The resolution of the monitoring device, specified as a string in the format "width x height" (e.g., "1920x1080", "1280x720").
- `frame_rate`: The frame rate of the monitoring device, specified in frames per second (fps).
- `connection_type`: The type of connection used by the monitoring device (e.g., "usb", "network").
- `device_id` or `ip_address`: The device ID or IP address of the monitoring device, depending on the connection type.
- `port`: The port number used for network connections, if applicable.
- `commands`: The available commands for controlling the monitoring device.
 - Each command is defined as a key-value pair, with the command name as the key and its properties as the value.
   - `function`: The name of the function to be executed when the command is called.
   - `async`: A boolean value indicating whether the command should be executed asynchronously.

### 9. Security

The `security` section defines the security settings for XMCode. It includes the following properties:

- `xmcode_security`: The security settings for XMCode.
 - `mode`: The security mode, which can be set to either "secure" or "encrypted".
 - `algorithm`: The encryption algorithm used when the mode is set to "encrypted" (e.g., "aes-256").

### 10. Synchronization

The `synchronization` section defines the time synchronization settings for XMCode. It includes the following properties:

- `time_synchronization`: The time synchronization settings.
 - `enabled`: A boolean value indicating whether time synchronization is enabled or disabled.
 - `start_time`: The start time for time synchronization, specified in the format defined by `time_format`.
 - `time_format`: The format of the time values used for time synchronization (e.g., "HH:mm:ss.SSS" for hours, minutes, seconds, and milliseconds).

### 11. User

The `user` section includes user-specific settings, such as the timezone.

- `timezone`: The timezone setting for the user (e.g., "UTC", "America/New_York").

## Attributes

The `attributes` section in the `settings.json` file provides additional information about the machine's physical characteristics and capabilities. It includes sub-sections for:

- `machine`: Overall attributes of the machine.
 - `accuracy`: The accuracy of the machine.
   - `linear`: The linear accuracy of the machine, specified in the unit of measurement (e.g., millimeters).
   - `angular`: The angular accuracy of the machine, specified in the unit of measurement (e.g., degrees).
 - `repeatability`: The repeatability of the machine.
   - `linear`: The linear repeatability of the machine, specified in the unit of measurement.
   - `angular`: The angular repeatability of the machine, specified in the unit of measurement.
- `axes`: Attributes specific to each axis.
 - Each axis is defined as a key-value pair, with the axis name as the key and its attributes as the value.
   - `max_speed`: The maximum speed of the axis, specified in the unit of measurement per second (e.g., mm/s, degrees/s).
   - `acceleration`: The maximum acceleration of the axis, specified in the unit of measurement per second squared (e.g., mm/s², degrees/s²).
   - `steps_per_mm`: The number of steps required for the axis to move one millimeter.
   - `backlash_compensation`: The backlash compensation value for the axis, specified in the unit of measurement.
- `tooling`: Attributes specific to each tooling.
 - Each tooling type is defined as a key-value pair, with the tooling name as the key and its attributes as the value.
   - For example, attributes for a `mill` tooling could include:
     - `spindle_power`: The power rating of the mill's spindle motor, specified in watts.
     - `spindle_runout`: The maximum runout of the mill's spindle, specified in the unit of measurement.
     - `tool_holder_type`: The type of tool holder used by the mill (e.g., "ER20", "ISO 40").
     - `tool_change_time`: The time required for a tool change operation, specified in seconds.
- `gearboxes`: Attributes specific to each gearbox.
 - Each gearbox is defined as a key-value pair, with the gearbox name as the key and its attributes as the value.
   - `type`: The type of gearbox (e.g., "planetary", "spur", "harmonic").
   - `ratio`: The gear ratio of the gearbox.
   - `max_torque`: The maximum torque that the gearbox can handle, specified in the unit of measurement (e.g., N·m).
   - `efficiency`: The efficiency of the gearbox, specified as a decimal value between 0 and 1.

## XMCode JSON

The `xmcode.json` file contains the actual commands and parameters for controlling the machine. It follows a structured format and includes sections for axes movement, tooling commands, custom commands, and synchronization.

The detailed structure and usage of the `xmcode.json` file will be covered in a separate section of the documentation.

## Conclusion

XMCode provides a comprehensive and flexible format for configuring and controlling various types of machines. By defining the machine's capabilities, limitations, and settings in the `settings.json` file, and using the `xmcode.json` file for actual machine control, XMCode enables advanced functionality, extensibility, and ease of use compared to traditional G-code.

For more detailed information on each section and property of the `settings.json` and `xmcode.json` files, please refer to the respective documentation sections.
