---
sidebar_position: 3
---

# Receive IMU Messages

Provides easy access to IMU data

:::info
The RAW IMU readings for a 9DOF sensor, which is identified by the id (default IMU1). This message should always contain the true raw values without any scaling to allow data capture and system debugging.
:::
:::note
See link for [detailed ](https://mavlink.io/en/messages/common.html#RAW_IMU) information. 
:::


| **Field Name** | **Type** | **Utils**                                                                                                                                                                            |
|:--------------:|:--------:|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| time_usec      | uint64_t | Timestamp (UNIX Epoch time or time since system boot). The receiving end can infer timestamp format (since 1.1.1970 or since system boot) by checking for the magnitude of the number. |
| xacc           | int16_t  | X acceleration (raw)                                                                                                                                                                   |
| yacc           | int16_t  | Y acceleration (raw)                                                                                                                                                                   |
| zacc           | int16_t  | Z acceleration (raw)                                                                                                                                                                   |
| xgyro          | int16_t  | Angular speed around X axis (raw)                                                                                                                                                      |
| ygyro          | int16_t  | Angular speed around Y axis (raw)                                                                                                                                                      |
| zgyro          | int16_t  | Angular speed around Z axis (raw)                                                                                                                                                      |
| xmag           | int16_t  | X Magnetic field (raw)                                                                                                                                                                 |
| ymag           | int16_t  | Y Magnetic field (raw)                                                                                                                                                                 |
| zmag           | int16_t  | Z Magnetic field (raw)                                                                                                                                                                 |
## Example


```jsx title="receive_imu_data.py"

import planekit

vehicle = planekit.Connection("tcp:127.0.0.1:5762")
vehicle.wait_heartbeat()
print("connection is successful")
while True:
    imu_message = vehicle.imu_message()
    print(imu_message.xacc)
    print(imu_message.yacc)
    print(imu_message.zacc)
    print(imu_message.xmag)
    print(imu_message.ymag)
    print(imu_message.zmag)
    print(imu_message.xgyro)
    print(imu_message.ygyro)
    print(imu_message.zgyro)
```

