# Pingr

**Monitor your servers from your pocket.**

Pingr is a mobile app that connects to your [Pingr agent](https://github.com/loutrx/pingr-api) to give you real-time visibility into your VPS health. No web dashboard, no browser tabs — just open the app, see your servers.

Built with Expo / React Native. Part of the [Otterium](https://otterium.com) ecosystem.

## Screenshots

> Coming soon

## Why a Mobile App?

Every monitoring tool gives you a web dashboard. But when your server goes down at 2am, you're not at your desk — you're reaching for your phone. Pingr is built for that moment: instant server status, push notifications, and quick actions like restarting a container, all from your phone.

## Features

### Dashboard
- **At-a-glance status** — green/yellow/red per server, see immediately if something needs attention
- **Server cards** — hostname, uptime, CPU/RAM/disk summary
- **Pull to refresh** — instant manual refresh

### Server Detail
- **Real-time metrics** — CPU, memory, disk, network with mini charts
- **Container list** — all Docker containers with status badges (running, stopped, unhealthy)
- **Health checks** — status of your monitored endpoints with response times
- **System info** — OS, kernel, Docker version, uptime

### Container Management
- **Container detail** — resource usage, ports, environment, created date
- **Live logs** — tail container logs directly from the app
- **Quick actions** — restart, stop, start a container with one tap + confirmation
- **Health status** — health check output if configured

### Health Checks
- **Endpoint list** — all monitored URLs with current status
- **Response time graph** — latency over time
- **Uptime percentage** — 24h / 7d / 30d
- **Status history** — timeline of up/down events

### Notifications
- **Push notifications** — instant alerts when something goes wrong
- **Configurable thresholds** — set per-server alert rules from the app
- **Alert history** — see what happened and when
- **Quiet hours** — mute notifications during specific time windows

### Multi-Server
- **Multiple agents** — add as many servers as you need
- **Server groups** — organize by environment (prod, staging, homelab)
- **Global overview** — all servers on one screen

## Tech Stack

- **Framework:** [Expo](https://expo.dev) (React Native)
- **Navigation:** [Expo Router](https://docs.expo.dev/router/introduction/)
- **State management:** Zustand or React Query
- **Charts:** react-native-chart-kit or Victory Native
- **Push notifications:** expo-notifications + Firebase Cloud Messaging
- **Storage:** expo-secure-store (API keys), MMKV (local cache)
- **Styling:** NativeWind (Tailwind for React Native) or StyleSheet

## Getting Started

### Prerequisites

- Node.js 18+
- Expo CLI (`npx expo`)
- A running [Pingr agent](https://github.com/loutrx/pingr-api) on your server

### Install

```bash
git clone https://github.com/loutrx/pingr-app.git
cd pingr-app
npm install
npx expo start
```

### Add a Server

1. Open the app
2. Tap **"Add Server"**
3. Enter your server IP/domain and port (default: 9009)
4. Enter your API key (shown during agent first run)
5. The app automatically registers for push notifications

Alternatively, the agent can display a QR code (`pingr qr`) that encodes the connection info for quick pairing.

## App Structure

```
pingr-app/
├── app/
│   ├── (tabs)/
│   │   ├── index.tsx              # Dashboard - server list overview
│   │   ├── alerts.tsx             # Alert history & notification settings
│   │   └── settings.tsx           # App settings, manage servers
│   ├── server/
│   │   └── [id]/
│   │       ├── index.tsx          # Server detail (metrics, containers, checks)
│   │       ├── container/
│   │       │   └── [containerId].tsx  # Container detail + logs
│   │       └── checks.tsx         # Health checks detail
│   ├── add-server.tsx             # Add/pair new server
│   └── _layout.tsx                # Root layout
├── components/
│   ├── ServerCard.tsx             # Server summary card for dashboard
│   ├── MetricGauge.tsx            # Circular gauge (CPU, RAM, disk)
│   ├── MiniChart.tsx              # Sparkline chart for metrics
│   ├── ContainerRow.tsx           # Container list item with status
│   ├── CheckRow.tsx               # Health check list item
│   ├── StatusBadge.tsx            # Running/stopped/unhealthy badge
│   └── AlertRow.tsx               # Alert history list item
├── lib/
│   ├── api.ts                     # Pingr API client
│   ├── store.ts                   # Zustand store (servers, settings)
│   ├── notifications.ts           # Push notification setup
│   └── types.ts                   # TypeScript types matching API responses
├── assets/
├── app.json
├── package.json
├── tsconfig.json
└── README.md
```

## Design Principles

- **Dark theme first** — monitoring apps are checked at night, be kind to eyes
- **Status at a glance** — color-coded everything: green = ok, yellow = warning, red = critical
- **Minimal taps** — most important info visible without drilling down
- **Offline resilience** — cache last known state, show stale data with timestamp rather than empty screens
- **Fast** — no loading spinners for cached data, background refresh

## Color Palette

| State | Color | Usage |
|-------|-------|-------|
| Healthy | `#10B981` (green) | Everything OK |
| Warning | `#F59E0B` (amber) | Approaching threshold |
| Critical | `#EF4444` (red) | Over threshold / down |
| Unknown | `#6B7280` (gray) | Unreachable / no data |
| Background | `#0F172A` (slate 900) | App background |
| Surface | `#1E293B` (slate 800) | Cards, panels |
| Text | `#F8FAFC` (slate 50) | Primary text |

## Roadmap

- [ ] Dashboard with server list
- [ ] System metrics display (CPU, RAM, disk, network)
- [ ] Docker container list and management
- [ ] Push notifications
- [ ] Multi-server support
- [ ] QR code pairing
- [ ] Health check history with charts
- [ ] WebSocket for live metric updates
- [ ] Widgets (iOS/Android home screen)
- [ ] Apple Watch / Wear OS complications
- [ ] Haptic feedback for status changes
- [ ] Biometric lock (Face ID / fingerprint) for container actions
- [ ] Share server access with team members (read-only)
- [ ] Localization (FR, EN, DE, ES)

## Distribution

- **iOS:** App Store via EAS Build
- **Android:** Google Play via EAS Build
- **Open beta:** Expo Go for quick testing

## Contributing

Contributions are welcome! Please read [CONTRIBUTING.md](CONTRIBUTING.md) before submitting a PR.

## License

AGPL-3.0-or-later — see [LICENSE](LICENSE)

---

Built with ☕ by [Otterium](https://otterium.com)
