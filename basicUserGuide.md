# Guide to Not Crashing Drones
## Some Basic Knowledge
- **What is Mission Planner? What is a transmitter?**
 Mission Planner is the software we use to monitor sensors and perform autonomous tasks and flight modes with the plane. [More info here](http://ardupilot.org/planner/docs/mission-planner-overview.html). A transmitter is that cool thing with joysticks that we use to control the planes manually. **We highly recommend that you practice with a transmitter and simulator first before flying any actual planes.**
- **Control Surfaces**
 These are the things that control the plane. They are called the ailerons, elevator, and rudder, which control roll, pitch, and raw, respectively. Roll, pitch, and yaw are rotation about the x, y, and z axis. [Here's a diagram.](https://upload.wikimedia.org/wikipedia/commons/thumb/c/c1/Yaw_Axis_Corrected.svg/2000px-Yaw_Axis_Corrected.svg.png)
- **Flight mode parameters** (the weird words in all caps) 
 These control various things about autonomous flight modes and failsafes. They can be found in Mission Planner under the top CONFIG/TUNING tab, and then under "Advanced Params" in the sidebar.

## Transmitter & Mission Planner Setup
**It is critical that you follow this correctly, otherwise control surfaces could reverse in different flight modes**

- link: [Servo and Transmitter Configuration](http://ardupilot.org/plane/docs/reversing-servos-and-setting-normalelevon-mode.html)

## Flight Mode Setup
### Loiter
[http://ardupilot.org/plane/docs/loiter-mode.html](http://ardupilot.org/plane/docs/loiter-mode.html)

This mode starts the plane circling around the point where loiter mode was engaged.

1. WP_LOITER_RAD
2. NAV_ROLL_CD
3. NAVL1_PERIOD
4. Altitude?

### FBWA
### RTL
### AUTO

## Sensor Setup
### Airspeed Sensor

## Failsafe
http://ardupilot.org/plane/docs/apms-failsafe-function.html

1. Set FS_GCS_ENABL to 1 to enable it.
2. Connect to the Mission Planner via telemetry. Verify on the bottom right corner of the HUD that you are “flying” in a non auto mode (Manual, Stabilize, FBW are ok).
3. Unplug one of the telemetry radios. After a few minutes power off your autopilot. (Remember the autopilot will not go into failsafe until FS_LONG_TIMEOUT seconds of MAVlink inactivity have passed).
4. Connect your autopilot to the mission planner and pull the logs. Verify on the log that the autopilot went into RTL after FS_LONG_TIMEOUT sec of MAVlink inactivity.
5. FS_SHORT_TIMEOUT: 1
6. FS_SHORT_ACTN: 0
7. FS_LONG_TIMEOUT: 5
8. FS_LONG_ACTN: 1
