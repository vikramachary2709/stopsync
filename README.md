# StopSync - Full-Stack Crowdsourced Transit Tracking Application

StopSync is a crowdsourced transit tracking web platform designed for municipal bus networks in developing cities where vehicles lack built-in GPS transponders. It empowers commuters to broadcast real-time location and occupancy data, enabling downstream riders to view accurate arrival countdowns and crowd levels at their stops.

## Application Architecture

```
stopsync-full-app/
├── index.html                  # Standalone executable prototype (double-click to run directly in any browser)
├── README.md                   # Complete documentation and setup guide
├── docs/
│   └── openapi.json            # OpenAPI 3.0 REST API specification
├── server/                     # Node.js + Express + SQLite REST Backend
│   ├── index.js                # REST API routes and periodic bus motion simulator
│   ├── db.js                   # SQLite database initializer and data access layer
│   ├── schema.sql              # Relational database schema definitions
│   ├── algorithms/
│   │   ├── etaEngine.js        # Haversine distance-velocity ETA heuristic
│   │   ├── pingValidator.js    # 200m polyline corridor validator & recency time decay
│   │   └── trafficAlerts.js    # Stationary bus (>10 min) gridlock alert detector
│   └── simulation/
│       └── busSimulator.js     # Autonomous polyline vehicle motion generator
└── client/                     # Modular React + Context API + Flexbox Frontend
    ├── package.json
    ├── css/
    │   └── style.css           # Responsive Flexbox, mobile navigation, and badge styles
    └── src/
        ├── App.jsx             # Main application wrapper and view router
        ├── context/
        │   └── TransitContext.jsx # Global state, LocalStorage bookmarks, and Karma points
        └── components/
            ├── Navigation.jsx    # Accessible header & navigation bar
            ├── RouteExplorer.jsx # Module 1 & 2: Interactive route corridors & timetables
            ├── LiveBoard.jsx     # Module 3: Next-bus countdown board & live/scheduled badges
            ├── CrowdPingModal.jsx# Module 4: 1-Tap location broadcast & battery saver mode
            └── SavedRoutes.jsx   # Bookmarked commute routes & Transit Karma badges
```

## Quick Start Guide

### Option 1: Standalone Demo (Zero Setup)
Double-click `index.html` in the root folder to open the full interactive StopSync application in any web browser instantly.

### Option 2: Production Development Mode
1. **Server Setup:**
   ```bash
   cd server
   npm install
   node index.js
   ```
2. **Client Setup:**
   ```bash
   cd client
   npm install
   npm run dev
   ```

## Grounded Features (per Hackathon Specification)
* **Modules 1–2 (Static Phase):** Interactive route map page with ordered stop nodes, responsive Flexbox layout, and structured timetable schedule grids.
* **Modules 3–4 (Dynamic Phase):** Route search with dynamic next-bus countdown board, 1-tap crowdsourced GPS location broadcast with battery-saver burst mode, crowd occupancy indicators (*Seats Available*, *Standing Only*, *Full/Crowded*), LocalStorage saved route quick access, and gamified Transit Karma rewards (+10 points per validated ping).
* **Stretch Features:** Offline browser timetable caching, Web Speech API audio arrival announcer, and stationary traffic jam detectors (>10 min delays).
