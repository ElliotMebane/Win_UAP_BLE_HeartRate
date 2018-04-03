# Unity Bluetooth LE HeartRate plugin for Windows/Hololens UWP apps 
  
Unity Store Link:  
https://assetstore.unity.com/packages/tools/input-management/hololens-heart-rate-monitor-plugin-76113  
  
Check here for the latest version of the plugin in case Unity has a delay in publishing it.  

The Plugin allows Unity apps for Windows or HoloLens/Mixed Reality to connect with external Bluetooth LE Heart Rate Monitors. This version of the plugin is free and a plugin with Pro features will be released soon.  

Pro Features coming soon:  
- Connect to a device without pairing it to your computer/HoloLens first.  
- Access to the complete raw byte array data coming from the device. Currently we return only the first 2 bytes of the array (the flags byte and the heart rate byte). Additional data that may come from devices (such as the Polar H7 chest strap) include inter-beat intervals (the time between each recent heart beat) which is good for HRV study (Heart Rate Variability), a measure of stress.

HRM Compatibility Testing -- Please report any other device combos you test.  
- Polar H& – Chest strap. The benchmark device I test with. Full support.  
- Zephyr HxM Smart – Tested on versions of the plugion prior to v1.3.4.0.   
- Zoom HRV – Wrist-worn PPG based HRM. Works.  
- Polar OH1 – Tested on Windows by a customer and confirmed to work.   
- Scosche Rhythm+ – Untested, however verified that the device sends data with a 00 flag byte followed by heart rate byte, so it should work as well as the Zoom HRV and Polar OH1 which both use the same 00 flag byte pattern.  
  
There are several applications I recommend for testing your HRM device's BLE capabilities:  
- Android/iOS – nRF Connect from Nordic Semiconductor:  
  - https://play.google.com/store/apps/details?id=no.nordicsemi.android.mcp&hl=en  
  - https://itunes.apple.com/us/app/nrf-connect/id1054362403?mt=8  
- Microsoft Bluetooth LE Explorer for Windows 10  
  - https://www.microsoft.com/en-us/store/p/bluetooth-le-explorer/9n0ztkf1qd98  
  
  
  
Release Notes  
   
1.3.4.0 (2018/04)  
- Updated and tested for the latest Microsoft Mixed Reality Toolkit, Unity, Windows OS, HoloLens OS, etc.  
- Added Windows 10 examples.  
- Expanded HRM device compatibility. Now compatibility with Zoom HRV watch and probably other HRMs that previously may not have worked.  
- The Plugin now simply disregards the flags byte and returns the value of the second byte as the heart rate. This is valid for most devices, however the full Bluetooth spec for Heart Rate Service allows the heart rate to be returned as 2-bytes, allowing for much faster heart rates (mainly for animals). Unfortunately, the ZoomHRV returns a flag byte of 00, which is pretty much nonsense according to the BLE spec and was causing an attempt to read heart rate from 2-bytes, but there was only one to read from. Also, in HRV mode the Zoom HRV broadcasts a flag byte of 10, which matches a SCOSCHE armband I recentlly tried. The new plugin has been tested with the Zoom HRV and works in both modes (active workout and HRV mode) that use flags 00 and 10, so it should work with a SCOSCHE armband as well.   
- I also removed the application of a gatt protection level. In prior versions it was set to expect an encrypted communication channel. Removing that was necessary to connect with the Zoom HRM, so I suspect their broadcast is not using the BLE encryption setting. For users who want to use one of the protection levels I've enabled it with a property “gattProtectionLevel” specified below.  
- Updated to conform to new Name reporting of Windows BLE. DeviceInformation.Name used to return the displayable name of the device, but now it returns “Heart Rate”. The displayable name must be retrieved for each DeviceInformation object in the list.   
- Added Advertisement Listening for RSSI updating.  
- Restricted the byte array data returned with receivedMeasurementData to only the first 2 bytes of the data (the flags byte and the heart rate byte).  
- Please use receivedMeasurementDataLimited now. Users who want RR data please contact me for a pro version of the plugin. 
 
1.2.0.0  
- Archive and Expose the un-processed Byte Array data received from the HRM device in a List: receivedMeasurementData  
- Added customizable size limit to the hrms and  receivedMeasurementData Lists  
- Added VERSION string   

1.1.2.0 Original release  
- Plugin Overview
- The Heart Rate Monitor plugin for Unity enables apps built for HoloLens and Windows 10 devices to receive data from an external Bluetooth LE Heart Rate Monitor.  

