---
sidebar_position: 4
---

# Receive AHRS Messages

Provides easy access to AHRS data

Provides easy access to GPS data

:::info
The global position, as returned by the Global Positioning System (GPS). This is NOT the global position estimate of the system, but rather a RAW sensor value.

:::
:::note
See link for [detailed ](https://mavlink.io/en/messages/common.html#GPS_RAW_INT) information. 
:::

|   **Field Name**   | **Type** | **Units** | **Description**                                                                                                                                                                            |    Values    |
|:------------------:|:--------:|:---------:|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:------------:|
| roll               | float    | rad       | Roll angle.                                                                                                                                                                                |              |
| pitch              | float    | rad       | Pitch angle.                                                                                                                                                                               | GPS_FIX_TYPE |
| yaw                | float    | rad       | Yaw angle.                                                                                                                                                                                 |              |
| altitude           | float    | m         | Altitude (MSL).                                                                                                                                                                            |              |
| lat                | int32_t  | degE7     | Latitude.                                                                                                                                                                                  |              |
| lng                | int32_t  | degE7     | Longitude.                                                                                                                                                                                 

## Example




```jsx title="receive_ahrs_data.py"

import planekit

import planekit

vehicle = planekit.Connection("tcp:127.0.0.1:5762")
vehicle.wait_heartbeat()
print("connection is successful")
while True:
    ahrs_message = vehicle.ahrs_message()
    print(ahrs_message.get_all_messages().roll)
    print(ahrs_message.get_all_messages().pitch)
    print(ahrs_message.get_all_messages().yaw)
    print(ahrs_message.get_all_messages().altitude)
    print(ahrs_message.get_all_messages().lat)
    print(ahrs_message.get_all_messages().lng)
  
```
