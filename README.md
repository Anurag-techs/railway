# Edge AI Railway Safety Control Panel Terminal

A production-quality frontend dashboard for an **Edge AI Railway Safety System**, built with **React**, **Vite**, and **Tailwind CSS**. It replicates an industrial control room monitoring railway corridors in real time.

---

## 🌟 Key Features

* **Real-time Telemetry Polling**: Polls the Edge AI backend (`status.json`) every second with cache-busting and connection-loss protection.
* **Dual Camera Feed Mode**:
  * **Canvas Track Simulator**: A dynamic HTML5 canvas rendering railway tracks, sleepers moving matching train motion, scanning HUD lines, and AI-detected obstacle bounding boxes (vehicle, debris, person) resizing dynamically by distance.
  * **Live IP Camera Stream**: Directly integrates a live stream from a configurable IP camera (e.g. MJPEG).
* **Industrial Safety Visuals**: Modern glassmorphic dark-theme console with tailored HSL status indicator signals (Green/Yellow/Red) and matching safety control commands (SAFE/SLOW/STOP).
* **ECG AI Heartbeat**: Live visual processor heartbeat using HTML5 Canvas indicating the connection's stability and risk-induced telemetry frequency (normal, rapid, or flatline).
* **Flashing Emergency Alerts**: Critical warning banner and full-screen flashing alerts coupled with synthesized dual-tone warning audio using the browser's Web Audio API.
* **Filterable Safety Event Log**: Table logging threat history with CSV export capabilities.
* **Flexible Configuration**: Full environment variable configurability for endpoints, app titles, polling rates, and default cameras.

---

## 🏗️ Folder Structure

```text
├── public/
│   └── status.json             # Telemetry data source (updated by simulator)
├── src/
│   ├── assets/                 # App assets & logos
│   ├── components/
│   │   ├── CameraFeed.jsx      # IP Stream feed and HTML5 railway simulator
│   │   ├── EventLog.jsx        # History log table & CSV export tool
│   │   ├── Header.jsx          # Title, live status, clocks, and theme settings
│   │   ├── StatusCards.jsx     # Risk level and control decision cards
│   │   └── SystemStats.jsx     # Scans tally, ECG heartbeat, and edge metrics
│   ├── hooks/
│   │   ├── useTelemetry.js     # Polling status, event logging, and stats
│   │   └── useAudioAlarm.js    # Dual-tone sound alarm synthesizer
│   ├── pages/
│   │   └── Dashboard.jsx       # Control Room Terminal dashboard layout
│   ├── App.jsx                 # Entrypoint page
│   ├── index.css               # Core styling and glassmorphism styling
│   └── main.jsx                # DOM mounting
├── .env                        # Local configurations
├── .env.example                # Configuration template
├── simulator.js                # Node telemetry simulator
├── tailwind.config.js          # Tailwind theme adjustments
└── package.json                # Project dependencies
```

---

## ⚙️ Environment Configurations

The dashboard properties are highly configurable. Copy `.env.example` into `.env` to customize settings:

| Variable | Description | Default Value |
| :--- | :--- | :--- |
| `VITE_APP_TITLE` | App Title displayed on the Header | `Edge AI Railway Safety System` |
| `VITE_STATUS_API_URL` | Telemetry endpoint path | `./status.json` |
| `VITE_POLL_INTERVAL_MS` | API request interval | `1000` |
| `VITE_DEFAULT_CAMERA_URL` | Default live IP camera stream URL | `""` |
| `VITE_SYSTEM_HOST` | Processor address shown in statistics | `http://localhost:5173` |

---

## 🚀 Getting Started

### Prerequisites
Make sure you have Node.js installed on your machine.

### 1. Install Dependencies
```bash
npm install
```

### 2. Start the Telemetry Simulator
The project includes a telemetry generator simulating railway hazards (pedestrians, stalled vehicles, landslides) and writing state updates to `public/status.json` every 1 second:
```bash
node simulator.js
```

### 3. Start the Vite Dev Server
In a separate terminal tab, spin up the React dev server:
```bash
npm run dev
```
Open your browser and navigate to the local server URL (e.g. `http://localhost:5173`).

### 4. Build for Production
To build static assets for hosting in industrial production networks:
```bash
npm run build
npm run preview
```
