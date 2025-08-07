# Example Missions

Currently, the flight stack offers the following built-in missions, provided the correct hardware is available:

!!! note
    TODO add screenshots of each in flight IRL

## Goal Point

Drop a point on the frontend map, and send a setpoint. If no DEM is included, no altitude adjustments are made. With DEM, the drone will stay within a predefined altitude volume AGL.

## Powerline Following

Detect powerlines in LiDAR and navigate along them, avoiding and mapping vegetation along the line.

!!! note
    Work in progress. Currently detects but does not send waypoints to follow.

## Trail Following

Detect trails in LiDAR and navigate along them, avoiding and mapping vegetation.

## Smart Lawnmower

This is an extension of the familiar lawnmower pattern, but with decision-making that enable the drone to adapt the path based on real-time conditions, e.g., to adjust for obstacles or cluttered environments. Any custom criteria can be added to enhance decision-making based on application-specific context. See the decision-making [development guide](../development/decisionmaking.md) for further instructions on adding your own.