# Hope Seeker AI 🆘

![Hope Seeker AI](https://img.shields.io/badge/Status-Active-brightgreen?style=for-the-badge)
![Node.js](https://img.shields.io/badge/Node.js-22-green?style=for-the-badge&logo=nodedotjs)
![Gemini AI](https://img.shields.io/badge/Gemini-2.0%20Flash-blue?style=for-the-badge&logo=google)
![India](https://img.shields.io/badge/Built%20For-India%20🇮🇳-orange?style=for-the-badge)

**Decentralized Disaster Relief Coordination Agent — Built for India**

Hope Seeker AI is a full-stack emergency coordination web application that allows citizens in distress to broadcast their GPS location and a voice note with a single click. An AI agent (powered by Google Gemini) orchestrates the response by classifying the emergency, routing it to the correct Indian authority (NDRF/SDRF, 108 EMS, 101 Fire, 112 ERSS), and alerting nearby volunteers in **bilingual English + Hindi**.

---

## 🏗️ Architecture

```
┌────────────────────────────────────────────────────────────┐
│                    Web Browser (Client)                    │
│  ┌─────────────┐  ┌──────────────┐  ┌───────────────────┐ │
│  │  SOS Button │  │ Leaflet Map  │  │ MediaRecorder API │ │
│  │ + Check-in  │  │ (Dark Matter)│  │ + SpeechRecognition│ │
│  └──────┬──────┘  └──────────────┘  └─────────┬─────────┘ │
└─────────┼──────────────────────────────────────┼───────────┘
          │ POST /api/emergency                   │ Audio Blob
          ▼                                       ▼
┌─────────────────────────────────────────────────────────────┐
│                   Express Server (Node.js)                  │
│  ┌──────────────┐  ┌─────────────────┐  ┌───────────────┐  │
│  │ Gemini 2.0   │  │ Haversine Dist. │  │ In-Memory DB  │  │
│  │ Flash (AI)   │  │ Smart Routing   │  │ Volunteers    │  │
│  │ - Transcribe │  │ NDRF/108/101/112│  │ Shelters      │  │
│  │ - Classify   │  │ Bilingual Alert │  │ Hazards       │  │
│  └──────────────┘  └─────────────────┘  └───────────────┘  │
└─────────────────────────────────────────────────────────────┘
```

## ✨ Features

| Feature | Description |
|---|---|
| 🆘 **One-Click SOS** | Records audio + GPS simultaneously |
| 🤖 **AI Classification** | Gemini classifies: Medical, Search & Rescue, Hazard, Basic Needs |
| 🗺️ **Live Leaflet Map** | Interactive dark map with emergency markers, volunteer paths, hazard icons |
| 🏥 **Smart Routing** | Auto-dispatches to closest NDRF/108/101/112 responder |
| 👥 **P2P Volunteer Broadcast** | Alerts volunteers within 2km radius |
| 🇮🇳 **Bilingual Alerts** | English + Hindi broadcast templates |
| ✅ **"I am Safe"** | Reassurance check-in with family broadcast |
| ⚠️ **Hazard Reporting** | Crowdsource waterlogging, road blockages, live wires |
| 🏫 **Shelter Directory** | NDRF Camps, Gurudwaras, Civil Defense Halls with resource tags |
| 🩺 **AI First-Aid Advice** | Immediate bilingual first-aid guidance by emergency type |
| 📵 **Offline Fallback** | Auto-generates SMS + WhatsApp emergency links when offline |

---

## 🚀 Quick Start

### Prerequisites
- Node.js v18+

### Setup

```bash
git clone https://github.com/YOUR_USERNAME/hope-seeker-ai.git
cd hope-seeker-ai
npm install
```

### Configure (Optional — for Gemini AI)

```bash
cp .env.example .env
# Add your GEMINI_API_KEY in .env
```

> Without an API key, the app runs in **Local Simulation Mode** using keyword-based NLP heuristics.

### Run

```bash
node server.js
```

Open **http://localhost:3000**

---

## 🧪 API Endpoints

| Method | Endpoint | Description |
|---|---|---|
| `POST` | `/api/emergency` | Main SOS handler — classify, route, broadcast |
| `GET` | `/api/volunteers` | List all registered volunteers |
| `POST` | `/api/volunteers` | Register a new volunteer |
| `GET` | `/api/shelters` | List all safe shelters |
| `GET` | `/api/hazards` | List all reported hazards |
| `POST` | `/api/hazards` | Report a new hazard |
| `POST` | `/api/check-in` | Register "I am Safe" check-in |
| `GET` | `/api/authorities` | List emergency authority agencies |
| `POST` | `/api/reset` | Reset simulation database to defaults |

---

## 🇮🇳 India-Specific Emergency Numbers

| Service | Number |
|---|---|
| Unified Emergency (ERSS) | **112** |
| Ambulance | **108 / 102** |
| Fire | **101** |
| Police | **100** |
| NDRF Helpline | **011-23438017** |

---

## ⚠️ Disclaimer

> Hope Seeker AI is an **AI-powered coordination prototype**. In life-threatening emergencies, always dial official emergency services (**112**) first.

---

## 📄 License

MIT License
