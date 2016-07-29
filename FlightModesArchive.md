# Flight Modes
This is an archive of the common pixhawk flight modes.  Use this in case ardupilot somehow gets deleted.

# Table of Contents
  * [Fly By Wire_A (FBWA)](#FBWA)
  * [Fly By Wire_B (FBWB)](#FBWB)
  * [Loiter](#Loiter)
  * [Circle](#Circle)
  * [Return to Launch (RTL)](#RTL)
  * [Auto](#Auto)
  * [Landing](#Landing)
  
<div id='FBWA'/>
## Fly By Wire_A (FBWA)
http://ardupilot.org/plane/docs/fbwa-mode.html

This is the most popular mode for assisted flying in Plane, and is the best mode for inexperienced flyers. In this mode Plane will hold the roll and pitch specified by the control sticks. So if you hold the aileron stick hard right then the plane will hold its pitch level and will bank right by the angle specified in the LIM_ROLL_CD option (in centidegrees). It is not possible to roll the plane past the roll limit specified in LIM_ROLL_CD, and it is not possible to pitch the plane beyond the LIM_PITCH_MAX/LIM_PITCH_MINsettings.

Note that holding level pitch does not mean the plane will hold altitude. How much altitude a plane gains or loses at a particular pitch depends on its airspeed, which is primarily controlled by throttle. So to gain altitude you should raise the throttle, and to lose altitude you should lower the throttle. If you want Plane to take care of holding altitude then you should look at the FlyByWireB mode.

In FBWA mode throttle is manually controlled, but is constrained by the THR_MIN and THR_MAX settings.

In FBWA mode the rudder is under both manual control, plus whatever rudder mixing for roll you have configured. Thus you can use the rudder for ground steering, and still have it used for automatically coordinating turns.

<div id='FBWB'/>
## Fly By Wire_B (FBWB) *UNTESTED*
http://ardupilot.org/plane/docs/fbwb-mode.html#fbwb-mode

The FBWB mode is similar to FLY BY WIRE_A (FBWA), but Plane will try to hold altitude as well. Roll control is the same as FBWA, and altitude is controlled using the elevator. The target airspeed is controlled using the throttle.

To control your altitude in FBWB mode you use the elevator to ask for a change in altitude. If you leave the elevator centred then Plane will try to hold the current altitude. As you move the elevator Plane will try to gain or lose altitude in proportion to how far you move the elevator. How much altitude it tries to gain for full elevator deflection depends on the FBWB_CLIMB_RATE parameter, which defaults to 2 meters/second. Note that 2 m/s is quite a slow change, so many users will want to raise FBWB_CLIMB_RATE to a higher value to make the altitude change more responsive.

Whether you need to pull back on the elevator stick or push forward to climb depends on the setting of the FBWB_ELEV_REV parameter. The default is for pulling back on the elevator to cause the plane to climb. This corresponds to the normal response direction for a RC model. If you are more comfortable with the reverse you can set FBWB_ELEV_REV to 1 and the elevator will be reversed in FBWB mode.

Note that the elevator stick does not control pitch, it controls target altitude. The amount of pitch that will be used to achieve the requested climb or descent rate depends on your TECS tuning settings, but in general the autopilot will try to hold the plane fairly level in pitch, and will primarily climb or descend by raising or lowering the throttle. This can be disconcerting for people used to flying in FBWA mode, where you have much more direct control over pitch.

If you have an airspeed sensor then the throttle will control the target airspeed in the range ARSPD_FBW_MIN to ARSPD_FBW_MAX. If throttle is minimum then the plane will try to fly at ARSPD_FBW_MIN. If it is maximum it will try to fly at ARSPD_FBW_MAX.

If you don’t have an airspeed sensor then the throttle will set the target throttle of the plane, and Plane will adjust the throttle around that setting to achieve the desired altitude hold. The throttle stick can be used to push the target throttle up beyond what it calculates is needed, to fly faster.

As with FBWA, the rudder is under a combination of manual control and auto control for turn coordination.

You should also have a look at CRUISE mode, as it is generally better than FBWB, especially if there is significant wind. In CRUISE mode the aircraft will hold a ground track as opposed to just levelling the wings when you don’t input any roll with the aileron stick.

<div id='Loiter'/>
## Loiter
http://ardupilot.org/plane/docs/loiter-mode.html#loiter-mode

In LOITER mode the plane will circle around the point where you started the loiter, holding altitude at the altitude that you entered loiter in. The radius of the circle is controlled by the WP_LOITER_RAD parameter, but is also limited by your NAV_ROLL_CD limit, and your :ref:`NAVL1_PERIOD` navigation tuning. As with Return To Launch (RTL) <rtl-mode> and AUTO mode you can “nudge” the plane while in LOITER using stick mixing, if enabled.

```
Warning

“Home” position is always supposed to be your Plane’s actual GPS takeoff location:

It is very important to acquire GPS lock before arming in order for RTL, Loiter, Auto or any GPS dependent mode to work properly.
For Plane the home position is initially established at the time the plane acquires its GPS lock. It is then continuously updated as long as the autopilot is disarmed.
This means if you execute an RTL in Plane, it will return to the location where it was when it was armed - assuming it had acquired GPS lock.
Consider the use of Rally Points to avoid returning directly to your arming point on RTL
```

<div id='Circle'/>
## Circle
http://ardupilot.org/plane/docs/circle-mode.html#circle-mode

Circle mode is similar to LOITER, but doesn’t attempt to hold position. This is primarily meant as a failsafe mode and is the mode that the aircraft will enter by default for 20 seconds when a failsafe event occurs, before switching to RTL.

Circle mode is deliberately a very conservative mode, and doesn’t rely on GPS positioning as it is used when GPS fails. It will do a large circle, The bank angle is set to the LIM_ROLL_CD divided by 3, to try to ensure the plane remains stable even without GPS velocity data for accelerometer correction. That is why the circle radius is so large.

Circle mode uses throttle and pitch control to maintain altitude at the altitude where it started circling.
<div id='RTL'/>

## Return to Launch (RTL)
http://ardupilot.org/plane/docs/rtl-mode.html#rtl-mode

In RTL mode the plane will return to its home location (the point where the plane armed - assuming it had GPS lock) and loiter there until given alternate intructions (or it runs out of fuel!). As with AUTO mode you can also “nudge” the aircraft manually in this mode using stick mixing. The target altitude for RTL mode is set using the ALT_HOLD_RTL parameter in centimeters.

Alternatively, you may configure the plane to return to a Rally Point, rather than the home location.

```
Warning

“Home” position is always supposed to be your Plane’s actual GPS takeoff location:

It is very important to acquire GPS lock before arming in order for RTL, Loiter, Auto or any GPS dependent mode to work properly.
For Plane the home position is initially established at the time the plane acquires its GPS lock. It is then continuously updated as long as the autopilot is disarmed.
This means if you execute an RTL in Plane, it will return to the location where it was when it was armed - assuming it had acquired GPS lock.
Consider the use of Rally Points to avoid returning directly to your arming point on RTL
```

<div id='Auto'/>
## Auto
http://ardupilot.org/plane/docs/auto-mode.html#auto-mode

In AUTO mode Plane will follow a mission (a set of GPS waypoints and other commands) set by your ground station. When entering AUTO mode Plane will continue from whatever mission item it was last doing, unless you have reset the mission.

When in AUTO Plane will by default allow the pilot to influence the flight of the plane by using “stick mixing”, which allows for aileron, elevator and rudder input to steer the plane in a way that can override the autopilot control. Whether this is enabled is determined by the STICK_MIXING option. By default stick mixing behaves the same as FLY BY WIRE_A (FBWA) mode.

```
Warning

“Home” position is always supposed to be your Plane’s actual GPS takeoff location:

It is very important to acquire GPS lock before arming in order for RTL, Loiter, Auto or any GPS dependent mode to work properly.
For Plane the home position is initially established at the time the plane acquires its GPS lock. It is then continuously updated as long as the autopilot is disarmed.
This means if you execute an RTL in Plane, it will return to the location where it was when it was armed - assuming it had acquired GPS lock.
Consider the use of Rally Points to avoid returning directly to your arming point on RTL
```
