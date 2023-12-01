# TimeProject for TwinCAT 3

## Overview
TimeProject is a comprehensive event logging and timestamping system built using TwinCAT 3. It is designed to operate within industrial automation environments, offering capabilities to monitor, record, and maintain a persistent history of events for subsequent analysis and review. 

![](https://i.imgur.com/s2u0Mlm.png)

## Objectives
The TimeProject aims to provide:
- **Event Logging**: Real-time capture of events, precise timestamp assignment, and immediate buffering for processing.
- **Persistent Storage**: Assurance that events are stored in a manner that allows them to persist through system restarts, available for recovery and analysis, typically in a CSV format.

Such a system is crucial in industrial settings for troubleshooting, conducting audits, process optimization, and meeting traceability and compliance requirements.
## Acknowledgments
This project is based on the educational content created by Jakob Sagatowski as part of his TwinCAT 3 tutorial series. All credit for the original concept and instructional design goes to him. 

Find his tutorials on [YouTube](https://www.youtube.com/playlist?list=PLimaF0nZKYHz3I3kFP4myaAYjmYk1SowO)

[<img src="https://i.imgur.com/7P9olxn.png" width="30%">](https://www.youtube.com/playlist?list=PLimaF0nZKYHz3I3kFP4myaAYjmYk1SowO "Tutorial - Pick&Place con RobotStudio de ABB (Proyecto Final)")

And **my notes** on these tutorials [here](https://mpatino-digital-garden.vercel.app/industrial-automation/plc-programming-courses/beckhoff/plc-programming-using-twin-cat-3-by-jakob-sagatowski/plc-programming-using-twin-cat-3-by-jakob-sagatowski-moc/).
## Requirements
**TwinCAT 3 Environment:**
```bash
System Manager Version: v3.1.0 (Build 4329)
TwinCAT Version: v3.1.4024.25
```

| Software/Package | Link |
| --------------------- | ------------------------------------------------------------------------------------- | 
| TwinCAT 3 | [Download TwinCAT 3](https://www.beckhoff.com/en-us/support/download-finder/) |
## Getting Started
To get started with the TimeProject, clone this repository and open the `.sln` file in TwinCAT 3. 
* Open the project in TwinCAT 3.
* Compile the project and load it onto your target PLC. 
* Ensure all dependencies, including `Tc2_Utilities`, are resolved.
## Dependencies
The project relies on several TwinCAT 3 libraries and external types. Ensure that the following are included in your environment before compiling and running the project:

- **Tc2_Utilities**: Used for handling file time (`FILETIME`) and converting it to DATE_AND_TIME format.
- **Tc2_System**: Contains function blocks such as `FB_FileOpen`, `FB_FilePuts`, and `FB_FileClose` for file operations.
- **Tc2_Standard**: Provides standard functions like `CONCAT` for string operations.

![](https://i.imgur.com/TWT6FyR.png)

- - -
## Usage
To log an event:
1. Set the appropriate variables for event type, severity, identifier, and text.
2. Call the `AddEvent` method on the `EventLogger` instance with these variables.

To view logged events:
1. Access the `Events.log` file in the specified directory of the PLC's file system.
- - - 
## Project Components

To facilitate a comprehensive understanding of the TimeProject's functionality and its codebase, I have provided a series of detailed diagrams along with their descriptions. Through these diagrams, users and developers can gain insights into the project's underlying structure, making it easier to navigate the code, implement modifications, or troubleshoot issues.

The following images depict the project's main components, their interconnections, and the flow of data across the system:

![](https://i.imgur.com/pBx4qCL.png)

### E_EventType and TcEventSeverity (Enums)
- `E_EventType`: An enumeration that defines the types of events, such as Alarms or Messages, enabling easy categorization and filtering of logged events.
- `TcEventSeverity`: An enumeration provided by the TwinCAT library that classifies the severity of an event into categories like Verbose, Info, Warning, Error, and Critical.

![](https://i.imgur.com/XPHXWcV.png)


### ST_Event (STRUCT)
A structured data type that encapsulates all necessary information about an event, including:
- `eEventType`: The event type from `E_EventType`.
- `eEventSeverity`: The event severity from `TcEventSeverity`.
- `nEventIdentity`: A unique identifier for the event.
- `sEvenText`: A descriptive text string describing the event.
- `dtTimestamp`: The date and time when the event occurred.

![](https://i.imgur.com/xVe8P96.png)

- - -
### UpdateEventTimestampWithSystemTime (FUNCTION)
This function let's us update an event's timestamp with the current system time to ensure accuracy.

![](https://i.imgur.com/Sgy1LVC.png)

### EventLogger (FB)
A function block responsible for:
- Buffering events with its `AddEvent` method.
- Initialization through `FB_init`, which links to persistent storage mechanisms.

![](https://i.imgur.com/sYTdhHe.png)

### FB_CsvPersistentEventStorage (FB)
Implements the `I_PersistentEventStorage` interface for persistent event storage, specifically:
- Writing events to a CSV file on the PLC's file system.
- Managing file operations through a state machine to open, write to, and close files systematically.

![](https://i.imgur.com/rWnUpav.png)

### I_PersistentEventStorage (INTERFACE)
Defines a standard contract for persistent event storage across different implementations, ensuring a consistent approach to event storage.

<img src="https://i.imgur.com/KGO7Ix2.png" width="50%">

### MAIN (PRG)
The main program that:
- Triggers event logging based on specific conditions.
- Ensures the `FB_CsvPersistentEventStorage` is executed in every PLC cycle for consistent logging and storage.

![](https://i.imgur.com/4tF8MR3.png)

- - -

## License
TimeProject is released under the [MIT License](LICENSE). It is shared for educational purposes and is not officially affiliated with Beckhoff or TwinCAT. Please use and share responsibly, giving credit to the original author and sources.

## Contact Information
You can contact me here:
* **LinkedIn:** https://www.linkedin.com/in/mauriliopatino97/
* **Email:** maurilio.pp97@gmail.com
* **Github:** https://github.com/Maurilio97-P
* **YouTube:** https://www.youtube.com/channel/UCLGiii_X3UzQe_fJH_CmQmw


