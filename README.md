<div align="center">

# Soundwave - Open Source Music Streaming Web App

**A cross-platform music player for web, desktop, and Android.**

![Version](https://img.shields.io/badge/version-1.5.0-blue?style=flat-square)
![React](https://img.shields.io/badge/React-20232A?style=flat-square&logo=react&logoColor=61DAFB)
![TypeScript](https://img.shields.io/badge/TypeScript-007ACC?style=flat-square&logo=typescript&logoColor=white)
![Electron](https://img.shields.io/badge/Electron-191970?style=flat-square&logo=electron&logoColor=white)
![Capacitor](https://img.shields.io/badge/Capacitor-119EFF?style=flat-square&logo=capacitor&logoColor=white)
![Firebase](https://img.shields.io/badge/Firebase-FFCA28?style=flat-square&logo=firebase&logoColor=black)

<img src="https://i.ibb.co/VpMJ7tRP/Screenshot-2026-06-14-180717.png" alt="Soundwave" width="100%" />

</div>

---

## Overview

Soundwave is a music player for streaming and managing your own library. It runs in the browser, as an Electron desktop app, and as an Android app through Capacitor. Firebase handles authentication, storage, and sync, so your library follows you across devices.

## Features

**Playback**
- MP3, WAV, FLAC and other browser-supported formats
- Seek, volume, shuffle, and repeat
- Real-time waveform and spectrum visualizer

**Library**
- Search and browse your songs
- Create, edit, and share playlists
- Bulk upload and cloud sync across devices
- Offline downloads

**Account**
- Google sign-in through Firebase Authentication
- Per-user profiles and libraries

**Extras**
- Voice commands (AssemblyAI)
- Sound Assistant for music recommendations
- Soundie Explorer for discovering music
- Light and dark themes
- Native media controls on Android

<div align="center">
  <img src="https://i.ibb.co/8T3jwmN/Screenshot-2026-10-17-113702.png" alt="Soundwave across devices" width="100%" />
</div>

---

## Tech Stack

| Layer | Technologies |
|-------|--------------|
| Frontend | React, TypeScript, Vite, Tailwind CSS, shadcn/ui, React Hook Form, Zod, Sonner |
| Backend | Node.js, Express, Firebase, Firebase Admin SDK, AssemblyAI |
| Desktop | Electron, Electron Builder |
| Mobile | Capacitor, Android SDK |
| Tooling | pnpm, Git, Vercel |

**Capacitor plugins:** `native-audio`, `screen-brightness`, `speech-recognition`, `capacitor-firebase/authentication`, `capgo/capacitor-media-session`

## Getting Started

### Requirements

- Node.js 18+
- pnpm 7+ (or npm 8+)
- A Firebase project ([console](https://console.firebase.google.com))
- Electron builds: platform build tools (Visual C++ Build Tools on Windows, Xcode CLT on macOS)
- Android builds: Android SDK (API 31+), JDK 11+, Gradle

### Install

```bash
git clone https://github.com/lonewolffsd/soundwave.git
cd soundwave
pnpm install
```

### Configure

```bash
cp .env.example .env.local
```

```env
VITE_FIREBASE_API_KEY=
VITE_FIREBASE_AUTH_DOMAIN=
VITE_FIREBASE_PROJECT_ID=
VITE_FIREBASE_STORAGE_BUCKET=
VITE_FIREBASE_MESSAGING_SENDER_ID=
VITE_FIREBASE_APP_ID=

VITE_ASSEMBLYAI_API_KEY=

REACT_APP_API_URL=http://localhost:3000
```

Firebase setup steps are in [docs/FIREBASE_SETUP.md](docs/FIREBASE_SETUP.md).

### Run

| Target | Command |
|--------|---------|
| Web (localhost:5173) | `pnpm run dev` |
| Backend (localhost:3000) | `pnpm run server` |
| Desktop | `pnpm run electron:dev` |
| Android | `npx cap sync && npx cap open android` |

## Building

| Target | Command | Output |
|--------|---------|--------|
| Web | `pnpm run build` | `dist/` |
| Desktop | `pnpm run electron:build` | `dist/` |
| Android (debug) | `./gradlew assembleDebug` | `app/build/outputs/` |
| Android (release APK) | `./gradlew assembleRelease` | `app/build/outputs/` |
| Android (Play bundle) | `./gradlew bundleRelease` | `app/build/outputs/` |

Deployment details are in [docs/DEPLOYMENT.md](docs/DEPLOYMENT.md).

---

## Project Structure

```
.
├── src/             React app (components, context, api, utils, pages)
├── components/      shadcn/ui component library
├── server/          Express backend and Firebase Admin setup
├── android/         Capacitor Android project
├── docs/            Setup and deployment guides
├── public/          Static assets
├── electron.js      Electron entry point
├── capacitor.config.ts
├── vite.config.ts
└── vercel.json
```

## API

Base URL: `http://localhost:3000`

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/songs/upload` | Upload a song |
| GET | `/api/songs` | List songs |
| GET | `/api/songs/:id` | Get song details |
| DELETE | `/api/songs/:id` | Delete a song |
| POST | `/api/songs/sync` | Sync library across devices |
| POST | `/api/playlists` | Create a playlist |
| GET | `/api/playlists` | List playlists |
| PUT | `/api/playlists/:id` | Update a playlist |
| DELETE | `/api/playlists/:id` | Delete a playlist |
| POST | `/api/playlists/:id/songs` | Add a song to a playlist |
| GET | `/api/user/profile` | Get profile |
| PUT | `/api/user/profile` | Update profile |
| POST | `/api/user/settings` | Save settings |

## Keyboard Shortcuts

| Key | Action |
|-----|--------|
| `Space` | Play / pause |
| `>` | Next song |
| `<` | Previous song |
| `M` | Mute / unmute |
| `F` | Toggle fullscreen |
| `Esc` | Close modals |

## Configuration

Mobile settings live in [capacitor.config.ts](capacitor.config.ts):

- App ID: `com.lonewolffsd.soundwave`
- App name: `Soundwave Music`
- Deployment URL: `https://soundwave.lonewolffsd.in`

Theme colors are set in [tailwind.config.js](tailwind.config.js).

## Troubleshooting

| Problem | Fix |
|---------|-----|
| Firebase fails to initialize | Check the credentials in `.env.local` and that the required Firebase services are enabled |
| No audio playback | Check browser audio permissions, CORS on audio URLs, and the Capacitor native audio plugin |
| Login redirect fails | Update OAuth redirect URIs in Firebase and the allowed navigation domains in Capacitor |
| Library not syncing | Check Firestore security rules, auth state, and network connection |
| Electron won't start | Run `pnpm run electron:dev` for logs and check your Node version |

For Android debugging, use `adb logcat`.

## Limitations

- Firebase free tier has storage limits
- AssemblyAI has usage limits
- Android only for mobile (iOS planned)
- Supported audio formats depend on the browser

## Roadmap

- [ ] Audio equalizer
- [ ] Collaborative playlists
- [ ] Desktop auto-updates
- [ ] Analytics dashboard
- [ ] iOS support

## Documentation

- [Getting Started](docs/GETTING_STARTED.md)
- [Firebase Setup](docs/FIREBASE_SETUP.md)
- [Deployment](docs/DEPLOYMENT.md)

## License

Private and proprietary. All rights reserved.

## Contact

- Email: [support@itzajx.in](mailto:support@itzajx.in)
- Website: [soundwave.lonewolffsd.in](https://soundwave.lonewolffsd.in)
- Issues: [GitHub Issues](https://github.com/lonewolffsd/soundwave/issues)

## Acknowledgments

[shadcn/ui](https://ui.shadcn.com/), [Capacitor](https://capacitorjs.com/), [Firebase](https://firebase.google.com/), [Vite](https://vitejs.dev/), [React](https://react.dev/)

---

<div align="center">

Built by Itz_Ajx

</div>
