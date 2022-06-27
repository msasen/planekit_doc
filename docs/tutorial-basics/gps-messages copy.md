---
sidebar_position: 2
---

# Receive GPS Messages

Provides easy access to GPS data

:::info
The global position, as returned by the Global Positioning System (GPS). This is NOT the global position estimate of the system, but rather a RAW sensor value.

:::
:::note
See link for [detailed ](https://mavlink.io/en/messages/common.html#GPS_RAW_INT) information. 
:::
|   **Field Name**   | **Type** | **Units** | **Description**                                                                                                                                                                            |  **Values**  |
|:------------------:|:--------:|:---------:|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:------------:|
| time_usec          | uint64_t | us        | Timestamp (UNIX Epoch time or time since system boot). The receiving end can infer timestamp format (since 1.1.1970 or since system boot) by checking for the magnitude of the number.     |              |
| fix_type           | uint8_t  |           | GPS fix type.                                                                                                                                                                              | GPS_FIX_TYPE |
| lat                | int32_t  | degE7     | Latitude (WGS84, EGM96 ellipsoid)                                                                                                                                                          |              |
| lon                | int32_t  | degE7     | Longitude (WGS84, EGM96 ellipsoid)                                                                                                                                                         |              |
| alt                | int32_t  | mm        | Altitude (MSL). Positive for up. Note that virtually all GPS modules provide the MSL altitude in addition to the WGS84 altitude.                                                           |              |
| eph                | uint16_t |           | GPS HDOP horizontal dilution of position (unitless * 100). If unknown, set to: UINT16_MAX                                                                                                  |              |
| epv                | uint16_t |           | GPS VDOP vertical dilution of position (unitless * 100). If unknown, set to: UINT16_MAX                                                                                                    |              |
| vel                | uint16_t | cm/s      | GPS ground speed. If unknown, set to: UINT16_MAX                                                                                                                                           |              |
| cog                | uint16_t | cdeg      | Course over ground (NOT heading, but direction of movement) in degrees * 100, 0.0..359.99 degrees. If unknown, set to: UINT16_MAX                                                          |              |
| satellites_visible | uint8_t  |           | Number of satellites visible. If unknown, set to UINT8_MAX                                                                                                                                 |              |
| alt_ellipsoid **   | int32_t  | mm        | Altitude (above WGS84, EGM96 ellipsoid). Positive for up.                                                                                                                                  |              |
| h_acc **           | uint32_t | mm        | Position uncertainty.                                                                                                                                                                      |              |
| v_acc **           | uint32_t | mm        | Altitude uncertainty.                                                                                                                                                                      |              |
| vel_acc **         | uint32_t | mm        | Speed uncertainty.                                                                                                                                                                         |              |
| hdg_acc **         | uint32_t | degE5     | Heading / track uncertainty                                                                                                                                                                |              |
| yaw **             | uint16_t | cdeg      | Yaw in earth frame from north. Use 0 if this GPS does not provide yaw. Use UINT16_MAX if this GPS is configured to provide yaw and is currently unable to provide it. Use 36000 for north. |              |
## Example


```jsx title="receive_gps_data.py"

import planekit

vehicle = planekit.Connection("tcp:127.0.0.1:5762")
vehicle.wait_heartbeat()
print("connection is successful")
while True:
    gps_message = vehicle.gps_message()
    print("lat:" + str(gps_message.lat))
    print("lon:" + str(gps_message.lon))
    print("alt:" + str(gps_message.alt))
    print("vel:" + str(gps_message.vel))
    print("all gps fata " + str(gps_message.message))
    print("time usec " + str(gps_message.message.time_usec))
    print("fix type " + str(gps_message.message.fix_type))
    print("eph " + str(gps_message.message.eph))
    print("epv " + str(gps_message.message.epv))
    print("satellites_visible " + str(gps_message.message.satellites_visible))
    print("alt_ellipsoid " + str(gps_message.message.alt_ellipsoid))
    print("h_acc" + str(gps_message.message.h_acc))
    print("v_acc" + str(gps_message.message.v_acc))
    print("vel_acc" + str(gps_message.message.vel_acc))
    print("hdg_acc" + str(gps_message.message.hdg_acc))
  
```
