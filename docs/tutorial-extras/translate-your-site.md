---
sidebar_position: 2
---

# Land
This function will make the landing at the desired coordinate.


```jsx title="land.py"
import planekit
import time

import planekit

vehicle = planekit.Connection("tcp:127.0.0.1:5762")
vehicle.wait_heartbeat()
print("connection is successful")

# vehicle.set_flight_mode("AUTO")
vehicle.takeoff_and_arm(400)
while 400 > vehicle.alt():
    time.sleep(0.1)
    print("takeoff: " + str(vehicle.alt()))


# vehicle.set_flight_mode("AUTO")
vehicle.land_and_disarm()

```

:::danger Uyarı
Land modunda iniş yapılacak konumun lat lon bilgisi **v0.2** sürümünde eklenecektir.
:::