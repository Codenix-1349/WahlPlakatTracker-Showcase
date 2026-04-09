# 📍 WahlplakatFinder

> A field-ready mobile app for documenting and managing election poster placements — built with React Native & Expo.

![Platform](https://img.shields.io/badge/platform-iOS%20%7C%20Android-lightgrey?style=flat-square&logo=apple&logoColor=white)
![Built with Expo](https://img.shields.io/badge/Expo%20SDK%2054-000020?style=flat-square&logo=expo&logoColor=white)
![React Native](https://img.shields.io/badge/React%20Native%200.81-20232A?style=flat-square&logo=react&logoColor=61DAFB)
![JavaScript](https://img.shields.io/badge/JavaScript-ES2024-F7DF1E?style=flat-square&logo=javascript&logoColor=black)
![Firebase](https://img.shields.io/badge/Firebase-ready-DD2C00?style=flat-square&logo=firebase&logoColor=FFCA28)
![Status](https://img.shields.io/badge/status-active%20development-brightgreen?style=flat-square)

---

## 📸 Screenshots

> _Screenshots follow shortly._

---

## 🧭 About

**WahlplakatFinder** is a cross-platform mobile application designed for campaign teams to efficiently record, track, and report the status of election posters in the field. Instead of paper lists or fragmented WhatsApp messages, teams get a structured, exportable overview — right from their pocket.

The app works **fully offline** and is ready to scale to cloud-backed team synchronization.

---

## ✨ Features

| Feature | Description |
|---|---|
| 📷 **One-tap capture** | Opens the camera immediately; GPS is fetched in parallel — no freezing, no waiting |
| 📍 **GPS + Reverse Geocoding** | Automatically resolves coordinates to a human-readable address |
| 🟢🔴 **Status tracking** | Mark each poster as **OK** or **Lost** with a single tap |
| 💬 **Comments** | Add free-text notes to any entry |
| 📄 **PDF Export** | Generates a clean, branded table ready to share via Mail or WhatsApp |
| 📊 **CSV / Excel Export** | Semicolon-separated, locale-aware (German decimal format) — opens directly in Excel |
| 📧 **Smart Share logic** | Single format → native share sheet; both formats → directly opens Mail with attachments |
| 💾 **Offline-first** | All data persists locally via AsyncStorage — no internet required |
| ☁️ **Firebase-ready** | Architecture supports seamless switch to Firestore cloud sync |

---

## 🏗️ Architecture

The project follows a clean separation of concerns with a **custom hooks pattern**:

```
src/
├── components/       # Pure UI components (ItemCard, Header, Modals)
├── hooks/            # Business logic
│   ├── useStorage    # AsyncStorage persistence layer
│   ├── useCapture    # Camera + GPS + Geocoding workflow
│   └── useExport     # PDF & CSV generation + smart sharing
├── screens/          # Screen-level layout (Main, Settings)
├── services/         # Firebase configuration (cloud-sync ready)
└── utils/            # Formatters, CSV helpers, navigation
```

**Key architectural decisions:**
- **Offline-First by default** — the app is fully functional without network access
- **Hooks over classes** — all side effects (storage, device APIs, exports) live in dedicated custom hooks, keeping screens lean and testable
- **Parallel execution** — camera and GPS permissions are handled in a UX-optimized sequence (camera first, GPS in background) to eliminate perceived wait times
- **Graceful degradation** — GPS timeout with retry, geocoding fallback to raw coordinates, entry without photo possible

---

## 🛠️ Tech Stack

<p align="left">
  <img src="https://skillicons.dev/icons?i=react,js,firebase,git,nodejs" />
</p>

| Package | Purpose |
|---|---|
| `expo-location` | GPS acquisition + reverse geocoding |
| `expo-image-picker` + `expo-file-system` | Camera capture & persistent local photo storage |
| `expo-print` | HTML-to-PDF rendering on-device |
| `expo-sharing` + `expo-mail-composer` | Cross-platform export & smart share logic |
| `@react-native-async-storage/async-storage` | Offline-first data persistence |
| `firebase` v12 | Firestore cloud sync (architecture ready, switchable) |
| `@expo/vector-icons` | Ionicons icon set |

---

## 🗺️ Roadmap

### ✅ v1.0 — MVP (current)
- [x] Offline-first data capture (photo + GPS + address)
- [x] Status management (OK / Lost)
- [x] Comment system
- [x] PDF & CSV export with smart sharing
- [x] Persistent local storage
- [x] Clean, field-usable UI

### 🔄 v1.5 — Cloud Sync & Teams *(in progress)*
- [ ] Firebase Firestore real-time sync
- [ ] Multi-user / multi-device support
- [ ] Shared campaign lists
- [ ] Firebase Storage for photo uploads

### 🚀 v2.0 — Advanced Features *(planned)*
- [ ] Map view with poster pins
- [ ] Filter & search within lists
- [ ] Push notifications (e.g. "poster reported lost")
- [ ] Role-based access (campaign manager vs. field worker)
- [ ] Analytics dashboard (coverage, loss rate by district)

---

## ⚙️ Setup

> **Note:** This project requires your own Firebase project. A `.env.example` is provided.

```bash
# Install dependencies
npm install

# Create your environment file
cp .env.example .env
# → Fill in your Firebase config in .env

# Deploy Firestore security rules
firebase deploy --project <your-project-id> --only firestore:rules

# Start the development server
npx expo start --clear
```

Scan the QR code with **Expo Go** on your device, or use `--tunnel` if on a restricted network.

---

## 📁 Export Format

### PDF
A formatted table including: entry number, address, GPS coordinates, timestamp, status, comment, photo indicator.

### CSV (Excel-compatible)
```
Nr;Zeit;Adresse;Status;Kommentar;Lat;Lng;Foto
1;22.03.2026 18:05;Musterstraße 12, Berlin;OK;Gut sichtbar;52,52000;13,40500;...
```

---

## 🔐 Environment Variables

```env
FIREBASE_API_KEY=
FIREBASE_AUTH_DOMAIN=
FIREBASE_PROJECT_ID=
FIREBASE_STORAGE_BUCKET=
FIREBASE_MESSAGING_SENDER_ID=
FIREBASE_APP_ID=
```

---

## 👤 Author

Developed independently as a field-tested solution for a real campaign use case — including active stakeholder involvement during development.

---

## 📄 License

This project is **not open source**. All rights reserved.