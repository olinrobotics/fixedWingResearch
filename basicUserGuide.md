# Guide to Not Crashing Drones
## Transmitter & Mission Planner Setup
**It is critical that you follow this correctly, otherwise control surfaces could reverse in different flight modes**

-link: [Servo and Transmitter Configuration](http://ardupilot.org/plane/docs/reversing-servos-and-setting-normalelevon-mode.html)

## Flight Mode Parameters
##### Loiter

## Sensor Parameters
##### Airspeed Sensor

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
