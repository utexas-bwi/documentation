

## Robot platforms
- BWIbot v4 uses the Segway RMP 220 V3 base by Stanley Innovation
- BWIbot v2 uses the Segway RMP 110 (todo: get details)

## BWIbot troubleshooting resources

Note that because these machines are no longer manufactured by Stanley Innovation, some links found in the manuals and wiki pages will be broken.  In particular, the Stanley Innovation github no longer has public repositories, and locating firmware is a challenge.

Manuals:
- https://github.com/utexas-bwi/documentation/tree/master/manuals

ROS wiki pages:
- [Robots/RMPv3](http://wiki.ros.org/Robots/RMPv3)
- [RMP 220 v3 troubleshooting](http://wiki.ros.org/Robots/RMPv3/indigo/troubleshooting)

ROS packages:
- [segway_v3](https://github.com/utexas-bwi/segway_v3) - this contains multiple packages from Stanley Innovation, including `segway_ros`.

## RMP 220 v3 : Read the fault log

- [ROS Wiki article](http://wiki.ros.org/Robots/RMPv3/indigo/reading_the_faultlog)

In most cases you'll have 30 seconds before the platform turns off.

```
cd segway_ws
sws
rosrun segway_ros segway_faultlog_parser
```

The faultlog is arranged with a header at the top and the 20 most recent faults below. The first fault logged is recorded as Fault[0],the second fault as Fault[1] and so on until the 20th fault is recorded as Fault[19]. At this point there are no empty slots remaining in the faultlog, so the 21st fault overwrites Fault[0]. Similarly, the 22nd fault overwrites Fault[1] in the log. This process continues indefinitely so that only the latest 20 faults are present in the log.

For your convenience the latest entry is listed in the header.  If a fault provides more information, that information is available in Data[0] and Data[1]. Often these contain bitmaps which can be decoded to provide additional information.

For a list of the types of faults, see the [Segway RMP 220 V3 Manual](https://github.com/utexas-bwi/documentation/tree/master/manuals), Page 53, Section "Troubleshooting".
