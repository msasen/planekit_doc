---
sidebar_position: 5
---

# Receive Heartbeat Messages

Provides easy access to Heartbeat data

:::info
The global position, as returned by the Global Positioning System (GPS). This is NOT the global position estimate of the system, but rather a RAW sensor value.

:::
:::note
See link for [detailed ](https://mavlink.io/en/messages/common.html#GPS_RAW_INT) information. 
:::

|  **Field Name** |         **Type**        |   **Values**  | **Description**                                                                                                                                                                                                                                                         |   |
|:---------------:|:-----------------------:|:-------------:|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:-:|
| type            | uint8_t                 | MAV_TYPE      | Vehicle or component type. For a flight controller component the vehicle type (quadrotor, helicopter, etc.). For other components the component type (e.g. camera, gimbal, etc.). This should be used in preference to component id for identifying the component type. |   |
| autopilot       | uint8_t                 | MAV_AUTOPILOT | Autopilot type / class. Use MAV_AUTOPILOT_INVALID for components that are not flight controllers.                                                                                                                                                                       |   |
| base_mode       | uint8_t                 | MAV_MODE_FLAG | System mode bitmap.                                                                                                                                                                                                                                                     |   |
| custom_mode     | uint32_t                |               | A bitfield for use for autopilot-specific flags                                                                                                                                                                                                                         |   |
| system_status   | uint8_t                 | MAV_STATE     | System status flag.                                                                                                                                                                                                                                                     |   |
| mavlink_version | uint8_t_mavlink_version |               | MAVLink version, not writable by user, gets added by protocol because of magic data type: uint8_t_mavlink_version                                                                                                                                                       |   |

## Example


```jsx title="receive_gps_data.py"
import planekit

vehicle = planekit.Connection("tcp:127.0.0.1:5762")
vehicle.wait_heartbeat()
print("connection is successful")
while True:
    ahrs_message = vehicle.heartbeat_message().get_all_state()
    print(ahrs_message.type)
    print(ahrs_message.autopilot)
    print(ahrs_message.base_mode)
    print(ahrs_message.custom_mode)
    print(ahrs_message.system_status)
    print(ahrs_message.mavlink_version)
```
