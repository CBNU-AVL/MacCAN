macOS Library for PCAN-USB Interfaces (x86_64)

Copyright (C) 2013-2017 by UV Software, Berlin


libPCBUSB
~~~~~~~~~

The PCBUSB library realizes a 'PCAN-USB Driver for macOS' using Apple�s IOUSBKit.
It supports up to 8 PCAN-USB or PCAN-USB FD devices from PEAK-System Technik.
See the header-file PCBUSB.h for details.

PCAN is a registered trademark of PEAK-System Technik GmbH, Darmstadt, Germany.
Mac and macOS are trademarks of Apple Inc., registered in the U.S. and other countries.

This software is freeware without any warranty or support!

Change-Log:
- Version 0.8 of 09/20/2017:
  Support of PCAN-USB FD devices in CAN 2.0 mode (CAN classic) and CAN FD mode!
  Adapted the API according to Peak's changes in version 4.2.0.134 and harmonized
  return codes with it.
  Fixed issue #208 'CAN_Write stuck when errors on the bus are present'.
  Conducted an intermediate solution for issue #246 (writing into a trace file).
  Added run-path-relative install name to the library (using the @rpath macro).
- Version 0.7 of 11/30/2016:
  Adapted the API according to Peak's changes in version 4.1.0.96 and harmonized
  return codes with it.
  Implemented parameter PCAN_CHANNEL_FEATURE and PCAN_BITRATE_INFO.
- Version 0.6 of 02/20/2015:
  Parameter PCAN_RECEIVE_EVENT returns a file descriptor to realize 'blocking
  read' by select() as on the Linux implementation of the PCAN-Basic API.
  Added two C++ examples and one Python example using the PCBUSB library.   
- Version 0.5 of 11/23/2014:
  Feature 'Reading/Writing of parameter PCAN_DEVICE_NUMBER' implemented.
  Fixed issue #104 'Hot plugging was not detected by the library/driver'.
  Fixed issue #117 'Permission for libPCBUSB.x.y.lib wrong' (chmod 755).
  Return codes of API functions harmonized with PCANBasic.dll (1.3.3.61).
- Version 0.4 of 02/23/2014:
  Time-stamps are now taken from CAN controller instead of taking them from the
  system clock. 
  Getting and setting of PCAN_* parameters reworked (to be almost compatible to
  the PCANBasic DLL, version 1.3)
  Resetting of RCV and XMT queue on the CAN controller realized.
- Version 0.3 of 11/02/2013:
  Fixed issue #11 'All channel initialized by the application will be closed
  even if they are in use'.
  CAN_Unitialize: closing all channel initialized by the application at once
  implemented.
  CAN_Read: receive queue overrun handling reworked.
  CAN_*: wrong function return codes corrected.
  CAN_GetErrorText: language support for English, German, French, Italian and
  Spanish added.
- Version 0.2 of 09/08/2013: 
  Minor changes
- Version 0.1 of 06/30/2013: 
  Initial revision

Limitations:
- CAN_Initialize:
  Only PCAN-USB devices and PCAN-USB FD devices are supported. 
- CAN_Write:
  Transmission of the given message on the CAN bus is not acknowledged by
  the USB interface.
- CAN_FilterMessages:
  Message filtering is currently not supported.
- CAN_GetValue/CAN_SetValue:
  Still unsupported parameter are: PCAN_5VOLTS_POWER, PCAN_MESSAGE_FILTER,
  PCAN_BUSOFF_AUTORESET, PCAN_LOG_*, PCAN_CONTROLLER_NUMBER,
  PCAN_CHANNEL_IDENTIFYING, PCAN_BITRATE_ADAPTING, PCAN_IP_ADDRESS,
  PCAN_LAN_SERVICE_STATUS, PCAN_ALLOW_STATUS_FRAMES PCAN_ALLOW_RTR_FRAMES,
  PCAN_ALLOW_ERROR_FRAMES, PCAN_INTERFRAME_DELAY, PCAN_ACCEPTANCE_FILTER_11BIT,
  PCAN_ACCEPTANCE_FILTER_29BIT.
- Writing into a trace file:
  Only 100'000 frames can be recorded into one trace file.
  An existing trace file with the same file name will be overwritten.

Known bugs and caveats
- The LED of the PCAN-USB FD device is not switch on (green) when the device
  is plugged into the USB. This is due to the fact that there is no 'driver'
  for PCAN-USB devices. So the LED of the PCAN-USB FD device cannot signal the
  presence of a driver. When operating the LED signals the correct operation
  state of the PCAN-USB FD device (blinking green, or red on error).
- The device number cannot be changed for PCAN-USB FD devices (function
  CAN_SetValue, parameter PCAN_DEVICE_NUMBER).
- When a successfully initialized PCAN-USB device is physically removed from
  USB any subsequent call of API functions (e.g. CAN_Read) will not succeed
  even when the device is plugged in again. An error code will be returned in
  this case.
- Due to the latency between the completions of the isochronous transaction on 
  the USB bus and servicing of the callback function, on slowed down systems a 
  mysterious repetition of already processed URBs may occur. In this case speed 
  up your system and everything works fine.


Contact
~~~~~~~

E-Mail:  mailto:info@mac-can.com
Internet: http://www.mac-can.com

