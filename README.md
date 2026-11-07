# HomeRun Map Card

An interactive map card for Philips HomeRun (Tuya) robot vacuums in Home Assistant, for the
[Philips HomeRun (Local)](https://github.com/coen1111/philips-homerun-xu7100-local) integration and
its [Home Assistant app](https://github.com/coen1111/HomeAssistantApps/tree/main/homerun-local).

Unofficial; not affiliated with Philips (Versuni) or Tuya.

## What it shows

- The stored map of each floor: rooms in colour, walls, the robot's own **no-go zones** and
  **virtual walls**, the dock, and the last run's route and end position.
- A **legend** where every layer has its own colour or icon; tap a chip to show or hide that layer.
- **Floor** chips for robots with a map per floor.
- Tap rooms to select them, then **Clean selected**; **Dock** and **Find** buttons.

## Installation

Through the Marketplace (HACS): add this repository as a custom repository with the category
**Dashboard**, then download **HomeRun Map Card**. The card is registered as a dashboard resource
automatically and shows up in the card picker.

Requires the **Philips HomeRun (Local)** integration (0.4.0 or newer) to be set up.

## Configuration

```yaml
type: custom:homerun-map-card
title: Timmy            # optional
hide: [route]           # optional; layers hidden until tapped in the legend:
                        # walls, nogo, vwalls, route, dock, robot, labels
entry: <entry id>       # optional; only needed with more than one robot
url: http://host:8787   # optional; call the backend directly instead of through Home Assistant
```

By default the card reaches the robot through Home Assistant, using your login, so it works on
https and away from home. With `url` it calls the backend directly, which only works on your own
network over plain http.

The floor choice is shared: switching floors in the card also switches the integration's
**Map floor** select and its map camera.
