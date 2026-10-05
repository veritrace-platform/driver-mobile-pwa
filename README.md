# VeriTrace Driver Mobile PWA

Mobile-first web application for drivers handling transport workflows in the VeriTrace platform.

This repository is currently the driver app scaffold. It contains the mobile route structure, PWA manifest, shared UI primitives, localization files, and planned feature boundaries. Most workflow pages and device integrations are still placeholders.

## Tech stack

- Next.js 14.2 with the App Router
- React 18 and TypeScript
- Tailwind CSS and shared shadcn-style UI components
- TanStack Query for server-state management
- Axios for HTTP integration
- Lucide React for icons

## Requirements

- Node.js 18.17 or newer
- pnpm

## Getting started

```bash
git clone https://github.com/veritrace-platform/driver-mobile-pwa.git
cd driver-mobile-pwa
pnpm install
pnpm dev
```

Open [http://localhost:3000](http://localhost:3000).

The current scaffold does not require environment variables. Add a local `.env.local` only when backend or device integrations are introduced; do not commit secrets.

## Available scripts

| Command | Purpose |
| --- | --- |
| `pnpm dev` | Start the development server |
| `pnpm build` | Create a production build |
| `pnpm start` | Serve the production build |
| `pnpm lint` | Run Next.js ESLint checks |

## Run with the enterprise dashboard

Both repositories default to port `3000`. Run the driver app on another port when developing both applications at once:

```bash
pnpm dev -- -p 3001
```

Open [http://localhost:3001](http://localhost:3001).

## Application structure

```text
src/
  app/
    driver/          Driver workflow routes
    [locale]/        Localized shared routes
    bff/              Backend-for-frontend route placeholders
    layout.tsx        Root layout
  components/
    mobile/           Mobile-specific components
    scanner/          Barcode scanning components
    temperature/      Temperature components
    location/         Location components
    feedback/         Driver feedback components
  features/           Driver domain boundaries
  lib/
    api/              API integration placeholder
    auth/             Authentication placeholder
    device/           Camera, barcode, geolocation, and vibration helpers
    gs1/              GS1 integration placeholder
    offline/          Connectivity and cache helpers
    realtime/         Realtime integration placeholder
  messages/            English and Vietnamese translation catalogs
public/
  manifest.webmanifest PWA metadata
```

## Driver routes

| Route | Purpose |
| --- | --- |
| `/driver` | Driver home |
| `/driver/trip` | Trip workflow |
| `/driver/scan` | Scan workflow |
| `/driver/handover` | Handover workflow |
| `/driver/alerts` | Driver alerts |
| `/[locale]/shipments/[id]` | Shipment details |

Routes are scaffolded and should be considered work in progress until their data, device, and offline flows are implemented.

## PWA and offline status

The app includes `public/manifest.webmanifest` with standalone display metadata. A production installable PWA also needs a service worker, suitable icons, HTTPS, and completed offline synchronization; those pieces are not configured in the current scaffold.

The following directories define planned device and offline boundaries:

- `src/lib/offline` for connectivity and local cache behavior
- `src/lib/device/camera` for camera access
- `src/lib/device/barcode` for barcode scanning
- `src/lib/device/geolocation` for location access
- `src/lib/device/vibration` for haptic feedback

Request device permissions only inside user-initiated workflows and provide a usable fallback when a capability is unavailable.

## Development guidelines

- Keep driver workflows under `src/features/<feature>` and route composition under `src/app`.
- Keep reusable mobile UI under `src/components`.
- Add translation keys to both `src/messages/en.json` and `src/messages/vi.json`.
- Treat offline writes as pending until they are confirmed by the backend.
- Keep credentials and environment-specific values out of source control.

## Validation

Run the following before opening a pull request:

```bash
pnpm lint
pnpm build
```

No dedicated test script is configured yet.

## Deployment

```bash
pnpm build
pnpm start
```

Deploy behind HTTPS when device APIs or PWA installation are enabled. Configure backend endpoints and secrets through the deployment environment when those integrations are added.

## Related application

The enterprise-facing dashboard lives in [enterprise-dashboard](https://github.com/veritrace-platform/enterprise-dashboard).
