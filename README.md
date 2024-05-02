# XMCode: Extended Machine Code

XMCode (Extended Machine Code) is a next-generation machine control format designed to provide a flexible and extensible way to configure and control various types of machines, including CNC machines, 3D printers, laser cutters, and robotic arms. It aims to address the limitations of traditional gcode and offer a more structured and readable format for machine control.

## Project Overview

The XMCode project consists of two main components:

1. **Settings JSON**: A comprehensive machine configuration file that defines the machine's capabilities, limitations, and settings. It includes information about axes, tooling, custom commands, and various machine-specific parameters.

2. **XMCode JSON**: A machine control file that contains the actual commands and parameters for controlling the machine. It uses a human-readable format and supports advanced features like parameter validation and asynchronous command execution.

The goal of XMCode is to provide a standardized and extensible format that can be easily adapted to different machines and use cases. It aims to simplify the process of configuring and controlling machines, while also enabling more advanced functionality and flexibility compared to traditional gcode.

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
     - Commands: Defines the available commands for the mill, such as on, off, and adjust speed, along with parameter validation and async flag.
   - Laser:
     - Maximum power: Specifies the maximum power output of the laser.
     - Wavelength: Indicates the wavelength of the laser.
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

3. **Custom Commands**: Allows defining custom commands that are not specific to any tooling.
   - Command name: Specifies the name of the custom command.
   - Function: Defines the function to be executed when the command is called.
   - Parameters: Specifies the parameters required for the command, including their types and ranges.
   - Async flag: Indicates whether the command should be executed asynchronously.

4. **Power-on Setup**: Defines the initial setup routine when the machine is powered on.
   - Enable/disable flag: Allows enabling or disabling the power-on setup routine.
   - Homing sequence: Specifies the order in which axes should be homed during the power-on setup.

5. **User Settings**: Includes user-specific settings.
   - Timezone: Specifies the timezone settings for the user.

The settings JSON file serves as a configuration template for the machine and can be easily modified to accommodate different machine types and configurations.

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
