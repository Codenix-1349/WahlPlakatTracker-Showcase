# 📍 WahlplakatFinder – Mobile Plakat-Dokumentation

Offline-fähige Feldapp für Wahlkampfteams · *React Native · Expo · Firebase · GPS · PDF/CSV-Export*

<img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/react/react-original.svg" width="40" title="React Native" />&nbsp;
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/javascript/javascript-original.svg" width="40" title="JavaScript" />&nbsp;
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/firebase/firebase-plain.svg" width="40" title="Firebase" />&nbsp;
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/git/git-original.svg" width="40" title="Git" />&nbsp;
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/nodejs/nodejs-original.svg" width="40" title="Node.js" />&nbsp;

---

## 📋 Inhaltsverzeichnis

- [Überblick](#überblick)
- [Screenshots](#screenshots)
- [App-Fluss im Detail](#app-fluss-im-detail)
- [Kernfunktionen](#kernfunktionen)
- [Technische Architektur](#technische-architektur)
- [Tech Stack](#tech-stack)
- [Setup](#setup)
- [Roadmap](#roadmap)
- [Was dieses Projekt zeigt](#was-dieses-projekt-zeigt)
- [Autor](#autor)

---

## <a id="screenshots"></a>📸 Screenshots

<table>
  <tr>
    <td align="center" width="50%">
      <img src="https://github.com/user-attachments/assets/a2292185-534e-41f6-a2c6-a8667c8e2504"
           width="300" alt="Eintrags-Liste" /><br/>
      <sub><b>Erfasste Plakate mit Status-Anzeige</b></sub>
    </td>
    <td align="center" width="50%">
      <img src="https://github.com/user-attachments/assets/d4593989-a24f-4480-ab56-8728c9ae0ce8"
           width="300" alt="Export-Dialog" /><br/>
      <sub><b>Export-Auswahl (PDF &amp; Excel)</b></sub>
    </td>
  </tr>
  <tr>
    <td align="center" colspan="2">
      <img src="https://github.com/user-attachments/assets/77a8fba6-8614-4b1c-bd38-3e2f31349c42"
           width="620" alt="Exportierte Liste" /><br/>
      <sub><b>Exportierte Plakat-Liste als PDF</b></sub>
    </td>
  </tr>
</table>

---

## <a id="überblick"></a>📖 Überblick

**WahlplakatFinder** ist eine cross-platform Mobile-App, die Wahlkampfteams ermöglicht, aufgehängte Wahlplakate strukturiert zu erfassen, ihren Status zu verfolgen und als Bericht weiterzuleiten — direkt aus dem Feld.

Statt Papierlisten oder Sammel-WhatsApp-Nachrichten entsteht eine saubere, exportierbare Übersicht in Sekunden:

```
Kamera öffnen → Foto machen → GPS + Adresse automatisch → Liste wächst
```

Das Projekt legt besonderen Wert auf:

- Sofortige Nutzbarkeit ohne Internetverbindung (Offline-First)
- Reibungslosen Kamera-GPS-Flow ohne Einfrieren oder Wartezeit
- Saubere Datenexporte direkt per Mail oder WhatsApp
- Erweiterbare Cloud-Architektur für zukünftigen Teamzugang

**Zielbereich:** Wahlkampforganisationen, Partei-Ortsverbände, Kampagnenteams jeder Größe.

---

## <a id="app-fluss-im-detail"></a>🔄 App-Fluss im Detail

### 🗳 Seite der Feldeinsatz-Teams

**1️⃣ App starten** — Keine Registrierung, keine Anmeldung nötig

**2️⃣ Plakate erfassen** — Ein Tap öffnet die Kamera; GPS + Adresse werden automatisch erkannt

**3️⃣ Status pflegen** — Jedes Plakat als OK oder Verloren markieren, Kommentar hinzufügen

**4️⃣ Bericht versenden** — Fertige Liste als PDF oder Excel exportieren und per Mail / WhatsApp teilen

---

### 📋 Seite der Wahlkampfleitung

**1️⃣ Teams einteilen** — Gebiete und Einsätze werden vorab außerhalb der App organisiert

**2️⃣ Bericht empfangen** — Das Feldteam schickt die exportierte Liste per Mail oder WhatsApp

**3️⃣ Auswerten** — PDF oder Excel direkt öffnen — Standorte, Status und Kommentare auf einen Blick

---

## <a id="kernfunktionen"></a>✨ Kernfunktionen

### 📷 Kamera & GPS

- Kamera startet sofort beim Tap — kein Einfrieren, kein Warten
- GPS wird parallel im Hintergrund geladen
- Automatische Reverse-Geocodierung: Koordinaten → lesbare Adresse
- Eintrag ohne Foto möglich (Rückfrage bei Kamera-Abbruch)
- GPS-Timeout mit Retry-Logik und Fallback auf Koordinaten

### 🟢🔴 Status & Kommentare

- Ein-Tap-Status-Toggle: **OK** oder **Verloren**
- Freitext-Kommentar pro Eintrag
- Nummerierte Liste für schnelle Übersicht im Feld

### 📤 Export-System

- **PDF-Export:** saubere Tabelle mit Adresse, GPS, Zeit, Status, Kommentar, Foto-Indikator
- **CSV/Excel-Export:** Semikolon-getrennt, deutsches Dezimalformat, direkt in Excel öffenbar
- **Smarte Share-Logik:** 1 Format → nativer Share-Dialog (WhatsApp sichtbar); beide Formate → direkt MailComposer mit Anhängen

### 💾 Offline & Persistenz

- Alle Daten lokal via AsyncStorage — komplett ohne Internet nutzbar
- Daten bleiben nach App-Neustart erhalten
- Firebase-Architektur vorhanden — Cloud-Sync per Schalter aktivierbar

---

## <a id="technische-architektur"></a>🧠 Technische Architektur

WahlplakatFinder ist nach dem Custom-Hooks-Pattern aufgebaut mit klarer Trennung zwischen UI, Logik und Datenhaltung.

```
Screens (UI)  →  Custom Hooks (Logik)  →  AsyncStorage / Firebase
```

```
src/
├── components/     # Reine UI-Komponenten (ItemCard, Header, Modals)
├── hooks/          # Gesamte Business-Logik
│   ├── useStorage  # Persistenz-Layer (AsyncStorage)
│   ├── useCapture  # Kamera + GPS + Geocoding-Workflow
│   └── useExport   # PDF & CSV-Generierung + Smart-Sharing
├── screens/        # Screen-Layout (Main, Settings)
├── services/       # Firebase-Konfiguration (Cloud-Sync ready)
└── utils/          # Formatter, CSV-Helfer, Navigation
```

**Architekturprinzipien:**

- Hooks over Classes — alle Seiteneffekte in dedizierten Hooks, Screens bleiben schlank
- Offline-First by Default — App funktioniert vollständig ohne Netz
- Parallele Ausführung — Kamera und GPS laufen entkoppelt, keine UX-Blockade
- Graceful Degradation — GPS-Timeout, Geocoding-Fallback, Speichern ohne Foto

---

## <a id="tech-stack"></a>🛠 Tech Stack

| Bereich        | Technologie                                              |
|----------------|----------------------------------------------------------|
| Framework      | React Native 0.81, Expo SDK 54                           |
| Sprache        | JavaScript (ES2024)                                      |
| Persistenz     | AsyncStorage (offline), Firebase Firestore (cloud-ready) |
| Kamera & GPS   | expo-image-picker, expo-location                         |
| Export         | expo-print, expo-file-system, expo-sharing               |
| Mail           | expo-mail-composer                                       |
| Icons          | @expo/vector-icons (Ionicons)                            |
| Cloud          | Firebase v12 (Firestore + Storage, architekturbereit)    |
| Versionierung  | Git                                                      |

---

## <a id="setup"></a>⚙️ Setup

> **Hinweis:** Das Projekt setzt ein eigenes Firebase-Projekt voraus. Eine `.env.example` liegt bei.

```bash
# Abhängigkeiten installieren
npm install

# Umgebungsdatei anlegen
cp .env.example .env
# → Firebase-Konfiguration in .env eintragen

# Firestore Security Rules deployen
firebase deploy --project <your-project-id> --only firestore:rules

# Entwicklungsserver starten
npx expo start --clear
```

QR-Code mit **Expo Go** scannen. Bei Netzwerkproblemen: `--tunnel` ergänzen.

---

## <a id="roadmap"></a>🗺 Roadmap

### ✅ v1.0 — MVP (aktuell)
- [x] Offline-First Erfassung (Foto + GPS + Adresse)
- [x] Status-Verwaltung (OK / Verloren)
- [x] Kommentar-System
- [x] PDF & CSV-Export mit Smart-Sharing
- [x] Persistente lokale Datenspeicherung
- [x] Maps-Deep-Link pro Eintrag — öffnet Standort direkt in Apple Maps / Google Maps (plattformabhängig mit Web-Fallback)
- [x] Sauberes, feldtaugliches UI

### 🔄 v1.5 — Cloud-Sync & Teams *(in Entwicklung)*
- [ ] Firebase Firestore Echtzeit-Synchronisation
- [ ] Multi-User / Multi-Gerät-Unterstützung
- [ ] Geteilte Kampagnenlisten
- [ ] Firebase Storage für Foto-Uploads

### 🚀 v2.0 — Erweiterte Features *(geplant)*
- [ ] **Navigationsroute zum Abhängen** — optimierte Fahrroute durch alle Plakatstandorte als Wegpunkte, sodass Teams die Strecke nur noch abfahren müssen
- [ ] In-App Kartenübersicht mit allen Plakat-Pins auf einen Blick
- [ ] Filter & Suche in Listen
- [ ] Push-Benachrichtigungen (z. B. „Plakat als verloren gemeldet")
- [ ] Rollenbasierter Zugang (Kampagnenleitung vs. Feldteam)
- [ ] Analyse-Dashboard (Abdeckung, Verlustquote nach Bezirk)

---

## <a id="was-dieses-projekt-zeigt"></a>🎯 Was dieses Projekt zeigt

- Custom-Hooks-Architektur mit klarer Single-Responsibility-Trennung
- Offline-First-Entwicklung mit AsyncStorage und Firebase-Migrations-Pfad
- UX-optimierter Kamera-GPS-Flow mit paralleler Ausführung und Fehlertoleranz
- Smarte Export-Logik mit kontextabhängigem Share-Verhalten (1 vs. 2 Formate)
- Produktreife App mit realem Stakeholder und konkreter Vermarktungsperspektive
- Vollständige React-Native-Entwicklung ohne Drittanbieter-UI-Framework

---

## <a id="autor"></a>👨‍💻 Autor

Eigenständig entwickelt als praxiserprobte Lösung für einen realen Wahlkampf-Use-Case — mit aktivem Stakeholder-Involvement während der Entwicklung.

GitHub: [github.com/Codenix-1349](https://github.com/Codenix-1349)
