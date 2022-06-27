---
sidebar_position: 1
---

# Go_to
Go to a specified global location.

If sleep equals is True, other commands are suspended until the UAV reaches the desired location.
If sleep equals is False then the UAV will execute the next command even if it has not reached the desired location yet.
```jsx
vehicle.go_to(lat, lon, alt, sleep=True)
```



```jsx title="takeoff.py"
import planekit

vehicle = planekit.Connection("tcp:127.0.0.1:5762")
vehicle.wait_heartbeat()
print("connection is successful")

# vehicle.set_flight_mode("AUTO")
vehicle.takeoff_and_arm(400)
while 400 > vehicle.alt():
    time.sleep(0.1)
    print("takeoff: " + str(vehicle.alt()))

vehicle.set_flight_mode("GUIDED")

vehicle.go_to(-35.3630510, 149.1654968, 578, sleep=True)

vehicle.go_to(-35.3649933, 149.1558409, 378, sleep=True)

# vehicle.set_flight_mode("AUTO")
vehicle.land_and_disarm()
```
