# XMCode: Extended Machine Code

XMCode (Extended Machine Code) is a next-generation machine control format designed to provide a flexible and extensible way to configure and control various types of machines, including CNC machines, 3D printers, laser cutters, and robotic arms. It aims to address the limitations of traditional G-code and offer a more structured and readable format for machine control.

## Project Overview

The XMCode project consists of two main components:

1. **Settings JSON**: A comprehensive machine configuration file that defines the machine's capabilities, limitations, and settings. It includes information about axes, tooling, sensors, custom commands, and various machine-specific parameters.

2. **XMCode JSON**: A machine control file that contains the actual commands and parameters for controlling the machine. It uses a human-readable format and supports advanced features like parameter validation and asynchronous command execution.

The goal of XMCode is to provide a standardized and extensible format that can be easily adapted to different machines and use cases. It aims to simplify the process of configuring and controlling machines, while also enabling more advanced functionality and flexibility compared to traditional G-code.

## Settings JSON

The settings JSON file is responsible for defining the machine's configuration and capabilities. It includes the following main sections:

1. **Axes**: Defines the properties and settings for each axis of the machine.
   - Motor type: Specifies the type of motor used for each axis (e.g., stepper, servo).
   - Drive type: Indicates the type of drive mechanism used for each axis (e.g., leadscrew, belt).
   - Range of motion: Defines the minimum and maximum limits for each axis, along with an enable/disable flag for hard limits.
   - Soft limits: Specifies the soft limits for each axis, which are used to restrict movement within a safer range, along with an enable/disable flag.
   - Homing direction: Indicates the direction of homing movement for each axis.
   - Homing speed: Specifies the speed at which homing is performed for each axis.
   - Limit switches: Defines the properties of limit switches for each axis, including enable/disable flag, triggered state, and last triggered time.

2. **Tooling**: Specifies the available tools and their associated settings.
   - Mill:
     - Maximum RPM: Defines the maximum rotational speed of the mill.
     - Horsepower: Specifies the power rating of the mill.
     - Tool offsets: Defines the offset values for each tool in the mill.
     - Wear compensation: Specifies the wear compensation values for the mill.
     - Commands: Defines the available commands for the mill, such as on, off, and adjust speed, along with parameter validation and async flag.
   - Laser:
     - Maximum power: Specifies the maximum power output of the laser.
     - Wavelength: Indicates the wavelength of the laser.
     - Tool offsets: Defines the offset values for the laser.
     - Commands: Defines the available commands for the laser, such as on, off, and set power, along with parameter validation and async flag.
   - 3D Printer:
     - Maximum temperature: Specifies the maximum temperature the 3D printer can reach.
     - Nozzle diameter: Defines the range of supported nozzle diameters.
     - Filament diameter: Indicates the diameter of the filament used.
     - Bed Leveling:
       - Enable/disable flag: Allows enabling or disabling bed leveling.
       - Grid size: Specifies the grid size used for bed leveling.
       - Last leveled time: Indicates the timestamp of the last bed leveling process.
       - Command: Defines the custom command for performing bed leveling.
     - Commands: Defines the available commands for the 3D printer, such as extrude, retract, and set temperature, along with parameter validation and async flag.

3. **Sensors**: Defines the available sensors and their configurations.
   - Limit switches:
     - Alias: Provides a user-friendly name for the limit switch.
     - Type: Specifies the type of sensor (e.g., limit switch).
     - Interface: Indicates the communication interface used by the sensor (e.g., digital, analog).
     - Pin: Specifies the pin to which the sensor is connected.
     - Axis: Indicates the axis associated with the limit switch.
     - Direction: Specifies the direction of the limit switch (e.g., min, max).
     - Triggered: Indicates whether the limit switch is currently triggered.
     - Last triggered: Stores the timestamp of the last trigger event.
     - Trigger actions: Defines the actions to be performed when the limit switch is triggered, including the condition, function to execute, and async flag.
   - Other sensors:
     - Alias: Provides a user-friendly name for the sensor.
     - Type: Specifies the type of sensor (e.g., temperature, color).
     - Interface: Indicates the communication interface used by the sensor (e.g., analog, I2C).
     - Pin or address: Specifies the pin or address to which the sensor is connected.
     - Response frequency: Defines how frequently the sensor provides updates or can be read.
     - Interpreter function: Specifies the function used to interpret the sensor's raw values into meaningful data.
     - Trigger actions: Defines the actions to be performed based on the sensor's interpreted data, including the condition, function to execute, and async flag.

4. **Custom Commands**: Allows defining custom commands that are not specific to any tooling.
   - Command name: Specifies the name of the custom command.
   - Function: Defines the function to be executed when the command is called.
   - Parameters: Specifies the parameters required for the command, including their types and ranges.
   - Async flag: Indicates whether the command should be executed asynchronously.

5. **Power-on Setup**: Defines the initial setup routine when the machine is powered on.
   - Enable/disable flag: Allows enabling or disabling the power-on setup routine.
   - Homing sequence: Specifies the order in which axes should be homed during the power-on setup.

6. **User Settings**: Includes user-specific settings.
   - Timezone: Specifies the timezone settings for the user.

The settings JSON file serves as a configuration template for the machine and can be easily modified to accommodate different machine types and configurations. It provides a comprehensive and structured way to define the machine's capabilities and settings.

## XMCode JSON

The XMCode JSON file contains the actual commands and parameters for controlling the machine. It follows a structured format and includes the following main sections:

1. **Axes**: Specifies the movement commands for each axis.
   - Target position: Defines the desired position for each axis.
   - Acceleration: Specifies the acceleration value for each axis movement.
   - Velocity: Indicates the velocity at which each axis should move.

2. **Tooling**: Defines the commands and parameters for the selected tooling.
   - Mill:
     - Command: Specifies the command to be executed, such as on, off, or adjust speed.
     - Parameters: Provides the necessary parameters for the command, such as RPM for adjust speed.
   - Laser:
     - Command: Specifies the command to be executed, such as on, off, or set power.
     - Parameters: Provides the necessary parameters for the command, such as power value for set power.
   - 3D Printer:
     - Command: Specifies the command to be executed, such as extrude, retract, or set temperature.
     - Parameters: Provides the necessary parameters for the command, such as length for extrude/retract or temperature for set temperature.

3. **Custom Commands**: Allows executing custom commands defined in the settings JSON file.
   - Command name: Specifies the name of the custom command to be executed.
   - Parameters: Provides the necessary parameters for the custom command.

4. **Async Flag**: Indicates whether the command should be executed asynchronously or not.

The XMCode JSON file is designed to be human-readable and easy to generate programmatically. It supports parameter validation and error handling based on the constraints defined in the settings JSON file.

## Attributes

The attributes section in the settings JSON file provides additional information about the machine's physical characteristics and capabilities. It includes the following main sections:

1. **Machine**: Defines the overall attributes of the machine.
   - Accuracy: Specifies the linear and angular accuracy of the machine.
   - Repeatability: Indicates the linear and angular repeatability of the machine.

2. **Axes**: Defines the attributes specific to each axis.
   - Maximum speed: Specifies the maximum speed achievable by the axis.
   - Acceleration: Indicates the maximum acceleration of the axis.
   - Steps per mm: Defines the number of steps required for the axis to move one millimeter.
   - Backlash compensation: Specifies the backlash compensation value for the axis.

3. **Tooling**: Defines the attributes specific to each tooling.
   - Mill:
     - Spindle power: Specifies the power rating of the mill's spindle.
     - Spindle runout: Indicates the maximum runout of the mill's spindle.
     - Tool holder type: Specifies the type of tool holder used by the mill.
     - Tool change time: Defines the time required for a tool change operation.
   - Laser:
     - Laser power: Specifies the maximum power output of the laser.
     - Focus diameter: Indicates the diameter of the laser's focused spot.
     - Pulse frequency: Defines the maximum pulse frequency of the laser.
     - Cooling system: Specifies the type of cooling system used by the laser.
   - 3D Printer:
     - Maximum print speed: Indicates the maximum printing speed of the 3D printer.
     - Maximum travel speed: Specifies the maximum non-printing movement speed.
     - Maximum acceleration: Defines the maximum acceleration of the print head.
     - Nozzle size: Specifies the diameter of the printer's nozzle.

The attributes section provides a way to capture the physical characteristics and capabilities of the machine and its components. These attributes can be used for reference, validation, or optimization purposes.

## Interpreter Functions

Interpreter functions are used to process and interpret the raw data received from sensors. They are defined in the settings JSON file and are associated with specific sensors. Interpreter functions take the raw sensor data as input and return meaningful values or labels based on the defined logic.

For example, an interpreter function for a color sensor might take the raw RGB values as input and return a color label such as "red," "green," or "blue" based on predefined thresholds. Similarly, an interpreter function for a temperature sensor might classify the temperature as "low," "normal," or "high" based on specified ranges.

Interpreter functions provide a way to abstract the low-level sensor data and convert it into more usable and meaningful information. They allow for customization and flexibility in interpreting sensor data based on the specific requirements of the machine and its application.

## Trigger Actions

Trigger actions are defined in the settings JSON file and are associated with sensors. They specify the actions to be performed when certain conditions are met based on the sensor's interpreted data.

Each trigger action consists of the following properties:
- Condition: Specifies the condition that must be satisfied to trigger the action. It can be a specific value or a range of values returned by the interpreter function.
- Function: Defines the function to be executed when the condition is met. This can be a custom function defined in the controller's code.
- Async flag: Indicates whether the function should be executed asynchronously or not.

Trigger actions allow for automated responses and behavior based on sensor input. For example, a trigger action for a limit switch might stop the associated axis when the switch is triggered. Similarly, a trigger action for a temperature sensor might adjust the bed temperature when it falls below or exceeds certain thresholds.

By defining trigger actions in the settings JSON file, the machine can be configured to perform specific actions based on sensor data without the need for explicit programming. This promotes modularity, reusability, and ease of configuration.

## Machine Control System

The XMCode format is designed to be used in conjunction with a machine control system that can interpret and execute the commands defined in the XMCode JSON files. The machine control system plays a crucial role in ensuring the safe and efficient operation of the machine. Here are some key aspects of the machine control system:

1. **Security**: The machine control system should implement appropriate security measures to protect against unauthorized access and malicious commands.
   - Authentication: Implement user authentication mechanisms to ensure that only authorized users can access and control the machine.
   - Command Validation: Validate incoming commands against the constraints and limits defined in the settings JSON file to prevent potentially harmful or invalid commands from being executed.
   - Data Encryption: Use secure communication protocols and encrypt sensitive data to protect against unauthorized interception or tampering.

2. **Custom Python Functions**: XMCode allows defining custom Python functions for executing specific commands or performing complex operations.
   - Function Definition: Custom Python functions can be defined in a separate Python file and referenced in the settings JSON file.
   - Parameter Passing: The machine control system should handle the passing of parameters from the XMCode JSON file to the corresponding Python functions.
   - Error Handling: Implement proper error handling mechanisms in the Python functions to gracefully handle exceptions and provide meaningful error messages.

3. **Real-time Feedback and Positional Updates**: The machine control system should provide real-time feedback and positional updates to ensure accurate tracking and monitoring of the machine's state.
   - Positional Feedback: After each command execution, the machine control system should respond with the current position of the machine's axes. This allows the client to track the machine's movement and verify that the commands are being executed correctly.
   - Status Updates: Implement mechanisms to send real-time status updates from the machine to the control system, including information about the current tooling state, any error conditions, and other relevant machine parameters.
   - Logging: Maintain detailed logs of machine activities, commands executed, and any errors or warnings encountered during operation.
   - Monitoring Dashboard: Develop a monitoring dashboard that displays real-time information about the machine's status, current job progress, and any relevant metrics.

4. **HTTP/API Integration**: The machine control system should provide native support for HTTP/API calls to enable seamless integration with external systems and remote control capabilities.
   - API Endpoints: Implement API endpoints that allow sending XMCode commands and receiving machine responses over HTTP.
   - Authentication and Security: Ensure that the API endpoints are secured using appropriate authentication mechanisms, such as API keys or token-based authentication, to prevent unauthorized access.
   - API Documentation: Provide comprehensive API documentation that describes the available endpoints, request/response formats, and any authentication requirements.

5. **Asynchronous Command Execution**: The machine control system should support asynchronous command execution to allow non-blocking operations and maintain a smooth motion loop.
   - Async Flag: Utilize the async flag in the XMCode JSON files to indicate which commands can be executed asynchronously without interrupting the main motion loop.
   - Background Processing: Implement a mechanism to process asynchronous commands in the background while the main motion loop continues executing.
   - Status Updates: Provide real-time status updates for asynchronous commands, including information about their execution progress and completion status.

6. **Modularity and Extensibility**: The machine control system should be designed with modularity and extensibility in mind.
   - Plugin Architecture: Implement a plugin architecture that allows adding new functionality or support for additional tooling without modifying the core system.
   - Configuration Management: Provide a configuration management system that allows easily updating and versioning the settings JSON file and other configuration files.
   - API Integration: Expose a well-defined API that allows integrating the machine control system with other software tools and systems.

7. **Safety Features**: Incorporate safety features into the machine control system to ensure safe operation and minimize the risk of accidents.
   - Emergency Stop: Implement an emergency stop mechanism that can immediately halt the machine's operation in case of any safety concerns or emergencies.
   - Limit Checks: Perform real-time limit checks to ensure that the machine operates within the defined soft and hard limits specified in the settings JSON file.
   - Failsafe Mechanisms: Implement failsafe mechanisms that automatically stop the machine or revert to a safe state in case of critical errors or loss of communication.

By addressing these aspects, the machine control system can provide a secure, flexible, and reliable environment for executing XMCode commands and controlling the machine effectively.

## Usage

To use XMCode in your machine control project:

1. Create a settings JSON file that defines your machine's configuration and capabilities.

2. Generate XMCode JSON files containing the desired commands and parameters for controlling your machine.

3. Develop a machine control software that can parse the settings JSON and XMCode JSON files, validate the commands and parameters, and execute them on your machine.

4. Integrate the XMCode format into your existing workflow or use it as a foundation for building new machine control systems.

## Contributing

Contributions to the XMCode project are welcome! If you have any ideas, suggestions, or bug reports, please open an issue or submit a pull request on the project's GitHub repository.

## License

The XMCode project is released under the [GNU General Public License v3.0](LICENSE).
