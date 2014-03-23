MAVROS
======

MAVLink extendable communication node for ROS
with UDP proxy for Ground Control Station (e.g. [QGroundControl][1]).


Feutures
--------

  * Communication with autopilot via serial port (e.g. [ArduPilot][2])
  * UDP proxy for Ground Control Station
  * [mavlink\_ros][3] compatible ROS topics (Mavlink.msg)
  * Plugin system for ROS-MAVLink translation
  * Parameter manipulation tool


Limitations
-----------

Only for linux. Depends on [Boost library][4] >= 1.49.
Catkin build system required (tested with ROS Hydro Medusa).


Parameters
----------

General node parametars:

  * ~/serial\_port -- FCU serial device (default: /dev/ttyACM0)
  * ~/serial\_baud -- serial baud rate (default: 57600)
  * ~/bind\_host -- UDP proxy listen host (default: 0.0.0.0)
  * ~/bind\_port -- UDP proxy port (default: 14555)
  * ~/gcs\_host -- GCS host
  * ~/gcs\_port -- GCS UDP port (default: 14550)
  * ~/system\_id -- Node MAVLink System ID (default: 1)
  * ~/component\_id -- Node MAVLink Component ID (default: 240 == UDP\_BRIDGE)
  * ~/target\_system\_id -- FCU System ID (default: 1)
  * ~/target\_component\_id -- FCU Component ID (default: 1)

Plugins parameters:

  * ~conn\_timeout -- FCU connection timeout \[sec\] (default: 30.0)
  * ~gps/frame\_id -- GPS Header.frame\_id (default: 'gps')
  * ~gps/time\_ref\_source -- TimeRefrence Header frame\_id (default: 'gps')
  * ~imu/frame\_id -- IMU Header.frame\_id (default: 'fcu')
  * ~imu/linear\_acceleration\_stdev -- accel's standard deviation (default: 0.0003)
  * ~imu/angular\_velocity\_stdev -- gyro's standard deviation \[rad\] (default: 0.02°)
  * ~imu/orientation\_stdev -- deviation for IMU.orientation (default: 1.0)
  * ~param/\* -- FCU parameters mapped by ParamPlugin
  * ~mission/pull\_after\_gcs -- automatically pull waypoints if GCS pulls (default: off)


Servicies
---------

ParamPlugin:

  * ~param/pull -- Pulls FCU params to rosparam
  * ~param/push -- Push rosparam to FCU
  * ~param/get -- Get one FCU parameter
  * ~param/set -- Set one FCU parameter and update rosparam with actual value

WaypointPlugin:

  * ~mission/pull -- Pulls FCU waypoints and publish
  * ~mission/push -- Push new waypoint list to FCU
  * ~mission/clear -- Clear waypoint list
  * ~mission/set\_current -- Set current active waypoint (in list)
  * ~mission/goto -- send one waypoint (only APM)


Testing
-------

Simple communication library test (serial-udp bridge):

    catkin_make mavudpproxy && ./devel/lib/mavros/mavudpproxy /dev/ttyACM0 115200


Links
-----

  * [MAVLink][5] -- communication protocol
  * [mavlink\_ros][3] -- original ROS node (few messages, no proxy)
  * [ArduPilot][2] -- tested autopilot APM:Plane (default command set)
  * [QGroundControl][1] -- tested ground control station for linux
  * [DroidPlanner][6] -- tested GCS for Android


[1]: http://qgroundcontrol.org/
[2]: http://ardupilot.com/
[3]: https://github.com/mavlink/mavlink_ros
[4]: http://www.boost.org/
[5]: http://mavlink.org/mavlink/start
[6]: https://github.com/arthurbenemann/droidplanner/
