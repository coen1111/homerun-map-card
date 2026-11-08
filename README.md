# HomeRun Map Card

An interactive map card for Philips HomeRun (Tuya) robot vacuums in Home Assistant, for the
[Philips HomeRun (Local)](https://github.com/coen1111/philips-homerun-xu7100-local) integration and
its [Home Assistant app](https://github.com/coen1111/HomeAssistantApps/tree/main/homerun-local).

Unofficial; not affiliated with Philips (Versuni) or Tuya.

## What it shows

- The stored map of each floor: rooms in colour, walls, the robot's own **no-go zones** (red),
  **no-mop zones** (blue) and **virtual walls**, the dock, and the last run's route and end position.
- A **legend** where every layer has its own colour or icon; tap a chip to show or hide that layer.
- **Floor** chips for robots with a map per floor.
- Tap rooms to select them, then **Clean selected**; **Dock** and **Find** buttons.

## Installation

Through the Marketplace (HACS): add this repository as a custom repository with the category
**Dashboard**, then download **HomeRun Map Card**. The card is registered as a dashboard resource
automatically and shows up in the card picker.

## How it reaches the robot

The card only ever talks to Home Assistant itself: the same address you opened Home Assistant on,
with your login. So it works the same on `homeassistant.local`, through Home Assistant Cloud and on
your own domain, and the app needs no port open to your network or the internet.

| `connection` | Route | Who |
|---|---|---|
| `auto` (default) | `proxy`, or `ingress` when the integration isn't set up | |
| `proxy` | The Philips HomeRun (Local) integration's authenticated proxy, `/api/homerun_local/proxy/…` | every user |
| `ingress` | The app's Supervisor ingress, `/api/hassio_ingress/…`, like the app's sidebar page | administrators |

## Configuration

```yaml
type: custom:homerun-map-card
title: Timmy            # optional
hide: [route]           # optional; layers hidden until tapped in the legend:
                        # walls, nogo, nomop, vwalls, route, dock, robot, labels
connection: auto        # optional; auto | proxy | ingress
entry: <entry id>       # optional; proxy, only with more than one robot
app: <app slug>         # optional; ingress, found by itself
url: http://host:8787   # optional; call the backend directly: its port must be open, this site
                        # in its cors_origins, and its API token below
token: <api token>      # optional; only with url
```

The floor choice is shared: switching floors in the card also switches the integration's
**Map floor** select and its map camera.
