---
sidebar_position: 1
---

# Takeoff 

This article explains how to get your plane to take off.

At high level, the steps are: check that the vehicle is able to arm, set the mode to AUTO, command the vehicle to arm, takeoff and block until we reach the desired altitude.

```jsx title="takeoff.py"
import planekit

vehicle = planekit.Connection("tcp:127.0.0.1:5762")
vehicle.wait_heartbeat()
print("connection is successful")

# vehicle.set_flight_mode("AUTO")
vehicle.takeoff_and_arm(400)
while 400 > vehicle.alt():
    print("takeoff: " + str(vehicle.alt()))

```
