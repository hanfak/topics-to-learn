# Mobile Architecture Checklist

<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Mobile Architecture Checklist](#mobile-architecture-checklist)
	- [Design Considerations](#design-considerations)
	- [Authentication and Authorization](#authentication-and-authorization)
	- [Caching](#caching)
	- [Communication](#communication)
	- [Configuration Management](#configuration-management)
	- [Data Access](#data-access)
	- [Debugging](#debugging)
	- [Deployment](#deployment)
	- [Device](#device)
	- [Exception Management](#exception-management)
	- [Logging](#logging)
	- [Porting](#porting)
	- [Power](#power)
	- [Synchronization](#synchronization)
	- [User Interface (UI)](#user-interface-ui)
	- [Performance Considerations](#performance-considerations)

<!-- /TOC -->

## Design Considerations

- What device types you will support?
- You have designed the application with occasionally-connected limited-bandwidth scenarios in mind.
- The user interface design is appropriate for the mobile device.
- You did not try to reuse a desktop application design or user interface.
- You have considered device resource constraints for battery life, memory size and program speed.

## Authentication and Authorization

- You have designed authentication for over-the-air, cradled synchronization scenarios, Bluetooth discovery, and local SD card scenarios.
- You have considered that different devices may have variations in their programming security model, which can affect authorization to access resources
- You did not assume that security mechanisms available on larger platforms will be available on a mobile platform.
- You have designed authentication for access to Bluetooth devices.
- Trust boundaries are identified within your mobile application layers.

## Caching

- Performance objectives are identified, such as minimum response time and battery life.
- You are caching static data that is useful, and avoided caching volatile data.
- You have considered data caching requirements for occasionally-connected scenarios.
- Your design supports low memory detection, and prioritization of data to discard, as available memory decreases.
- You chose the appropriate cache location, such as on the device, at the mobile gateway, or in the database server.

## Communication

- Your design supports asynchronous, threaded communication to improve usability in occasionally-connected scenarios.
- You have considered the effects of receiving a phone call during communication or program execution.
- Communication over un-trusted connections, such as Web services and other over-the-air methods, is protected.
- You have considered using Web services for communication when you must access data from multiple sources, interoperate with other applications, or work while disconnected.
- You have considered message queuing when you need guaranteed delivery, asynchronous messaging, message security, or transaction support.

## Configuration Management

- Your design supports the saving and restoration of configuration data after a device reset.
- Merge replication with a “buy and configure” application from a third party is used, if the enterprise data is in Microsoft SQL Server 2005 or 2008 and desire an accelerated time to market.
- You are using a binary format instead of XML for configuration files due to memory limitations.
- You are protecting sensitive data in device configuration files.
- You have considered using compression library routines to reduce the memory requirements for configuration and state information.
- You have considered using the Mobile Device Manager interface to manage group configuration of devices when you have an Active Directory infrastructure.

## Data Access

- You have designed application to ensure data integrity.
- You are using the device database services (such as SQL Server Compact Edition) when your application must access a disconnected database.
- You are using merge replication to synchronize large volumes of data in one operation over a high bandwidth network connection.
- You have considered the overall size and impact on performance when you use XML to store or transfer data.
- You are using custom data transfer objects instead of DataSets to reduce memory overhead and improve performance.
- You are using the Microsoft Sync Framework when you must synchronize individual sets of a data over a remote connection.

## Debugging

- You understand debugging costs associated with devices you need to support.
- You are using an emulator for initial testing and debugging.
- You are using the device for final testing.
- You have tested fully-disconnected scenarios in the design.
- You understand that it may be difficult to maintain context between different types of code running on a device.

## Deployment

- Your design supports over-the-air deployment when users must be able to install and update applications while away from the office.
- You are using ActiveSync to deploy your application when the application relies heavily on a host PC.
- You are using the post-load mechanism to automatically load your application immediately after the Windows Mobile OS starts up when you are deploying a baseline experience running on top of Windows Mobile.
- You have included multiple device executables in the CAB when you are using CAB file distribution.
- Application will be deployed using an SD memory card if the application will be run only at a specific site and you want to manually control distribution.
- Does the application function on JailBroken/Routed devices?

## Device

- The application is optimized for the device by considering factors such as screen size and orientation, network bandwidth, memory and storage space, and other hardware capabilities.
- Device-specific capabilities have been considered that will enhance your application functionality, such as accelerometers, GPUs, GPS, haptic (touch, force and vibration) feedback, compass, camera and fingerprint readers.
- You have designed a core functionality sub set when you are developing for more than one device.
- You have considered adding customization for device-specific features, including functionality to detect when the code is running on a device that can utilize this functionality.
- You have created modular code that can be removed if separate executable files are required due to device memory size constraints.
- Does the application make use of security features of the device to lock the sensitive date (e.g Keychain)?

## Exception Management

- Your application is designed to recover to a known good state after an exception.
- You did not use exceptions to control logic flow.
- Sensitive information in exception messages and log files are not revealed to users.
- Unhandled exceptions are dealt with appropriately.
- You have designed an appropriate logging and notification strategy for critical errors and exceptions.

## Logging

- You did not store sensitive information in log files.
- You have considered using the Mobile Device Manager to extract logs from mobile devices when you have an Active Directory infrastructure.
- You have considered using platform features such as health monitoring on the server, and mobile device services on the device, to log and audit events.
- You have considered logging in an abbreviated or compressed format to minimize memory and storage impact when you carry out extensive logging on the device.
- You have used OpenNetCF on the device if you do not require extensive logging.
- You have decided what constitutes unusual or suspicious activity on a device, and logged information based on these scenarios.

## Porting

- The application was re-written in its entirety when porting a Rich Client application from the desktop.
- The user interface has been redesigned for the smaller screen size when porting a Web application to a mobile device.
- You have researched details to discover what code will port without modification when porting a RIA client.
- You have researched and utilized tools to assist in porting.
- You have tested the custom controls which when porting to a mobile application and based on the results decided to rewrite to find an alternative.

## Power

- The user interface is not updated while the application is in the background.
- Communication methods that use the least amount of power necessary are used.
- Power profiles have been implemented to increase performance when device is plugged into external power and not charging the battery.
- Power consumption has been considered when using the device CPU, wireless communication, screen, or other power-consuming resources while on battery power.
- Device functionality is allowed to be powered down when not in use or not needed. Common examples are screen backlighting, hard drives, GPS functions, speakers, wireless communications.

## Synchronization

- Your design supports recovery when synchronization is reset, and is able to manage synchronization conflicts.
- You have considered the Microsoft Sync Framework when you want easy-to-implement one-way synchronization.
- You have considered using merge replication synchronization when you must support bidirectional synchronization to SQL Server.
- You have considered including over-the-air synchronization in your design when users must synchronize data when away from the office.
- You have considered including cradled synchronization in your design when users will be synchronizing with a host PC.
- You have considered store and forward synchronization using WCF over email or SMS (text message) mechanisms.

## User Interface (UI)

- You have provided the user with a visual indication of blocking operations; for example, an hourglass cursor.
- You did not place menu bars at the top of the screen as they are difficult to see when using a stylus or touch screen input.
- The design of your layout considers input from various sources. For example, making buttons large enough for devices that supports touch screen.
- Your design supports various screen sizes and orientations associated with devices you need to support.

## Performance Considerations

- Your design supports configurable options to allow the maximum use of device capabilities.
- You have considered using lazy initialization to optimize for mobile device resource constraints.
- You have considered limited memory resources and optimized your application to use the minimum amount of memory.
- You have considered using programming shortcuts as opposed to following pure programming practices that can inflate code size and memory consumption.
- You have balanced performance requirements with power consumption requirements.
