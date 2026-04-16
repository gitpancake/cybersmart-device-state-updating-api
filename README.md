# cybersmart-device-state-updating-api

**Archived.** The State API for **CyberSmart** — a smart-home IoT system developed as a University Group Project. The central choke-point for device-state changes: accepts state updates from nodes and pushes new state out to target devices.

## About CyberSmart

CyberSmart is a low-cost, low-resource, eco-friendly smart-home system built on a suite of independent Node.js microservices and Raspberry Pi hardware. A central **hub** (Raspberry Pi 3 Model B) runs the microservices backend and talks to lightweight **nodes** (Raspberry Pi Zero, running Jessie Pixel Headless) over a RESTful protocol.

## What this repo is

Express + MongoDB service that:

- **Receives** state updates from device nodes on the network (every 30-minute poll, plus ad-hoc changes)
- **Pushes** state changes out — accepts an IP + new state from the UI, then POSTs that state to the target node's endpoint
- Persists state history with timestamps in MongoDB

This is the bridge between the UI layer (humans triggering state changes) and the physical node layer (Raspberry Pi devices actually switching GPIO pins).

## Tech stack

- **Node.js** + **Express**
- **Mongoose** (MongoDB)
- **axios** for outbound calls to device nodes
- **body-parser**, **compression**, **cors**

## Structure

```
server.js           # Express app entry
Routes/             # HTTP endpoints
Handlers/           # Business logic
Models/             # Mongoose schemas (state history)
Services/           # Outbound HTTP client for calling node endpoints
```

## Running

```bash
npm install
node server.js
```

## Related repositories

The CyberSmart ecosystem:

- [`cybersmart-ui`](https://github.com/gitpancake/cybersmart-ui) — React frontend
- [`cybersmart-devices-api`](https://github.com/gitpancake/cybersmart-devices-api) — Express API for managing devices
- [`cybersmart-users-api`](https://github.com/gitpancake/cybersmart-users-api) — user management API (bcrypt + passport-jwt)
- [`cybersmart-locations-api`](https://github.com/gitpancake/cybersmart-locations-api) — API for managing locations within the home
- [`cybersmart-gpio-node`](https://github.com/gitpancake/cybersmart-gpio-node) — the node software that runs on each Raspberry Pi (the target of this service's outbound state-push calls)
- [`nodejs-logger-api`](https://github.com/gitpancake/nodejs-logger-api) — CyberSmart-Logger-API — centralized logging service
