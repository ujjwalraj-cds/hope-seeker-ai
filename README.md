# 🆘 Hope Seeker AI

> **AI-powered disaster relief coordination platform designed to help people report emergencies, understand incidents, and connect with nearby responders faster.**


\

**Hope Seeker AI** is a disaster-response prototype built around a simple idea:

> **When someone needs help during a disaster, reporting the problem should be as fast and simple as possible.**

The platform combines **AI-assisted incident understanding, geolocation, proximity-based responder matching, emergency guidance, and disaster mapping** into a single web application.

🚧 **Project Status:** Functional MVP / actively under development.

---

## 🚀 Live Demo

### Try the deployed application

**[Launch Hope Seeker AI →](https://hope-seeker-ai.onrender.com)**

The deployed version demonstrates the complete emergency-reporting workflow using the project's current prototype data and services.

> **Note:** This is a prototype and is **not connected to official emergency dispatch infrastructure**. Responder, shelter, and emergency-service data used by the application may be simulated/local data.

---

## 🎥 Demo

*Add a short screen recording or GIF of the application here.*

Recommended demo flow:

```text
Emergency Dashboard
        ↓
Create SOS / Emergency Report
        ↓
Capture Location
        ↓
Voice / Text Description
        ↓
AI Incident Classification
        ↓
Priority & Incident Type
        ↓
Nearby Responder Matching
        ↓
Emergency Guidance
        ↓
Incident Resolution
```

---

## 🎯 The Problem

During disasters such as floods, earthquakes, fires, or other emergencies, people can struggle to communicate:

* **What happened**
* **Where they are**
* **What kind of help they need**
* **How urgent the situation is**
* **Who nearby can help**

Traditional emergency communication can also become difficult when information is incomplete, unstructured, or provided under stress.

Hope Seeker AI explores whether an AI-assisted system can simplify the first stage of emergency coordination.

---

## 💡 The Solution

Hope Seeker AI provides a unified interface where a user can submit an emergency report and provide information such as:

* Current location
* Voice or text description
* Emergency category
* Optional additional information

The backend processes the report and combines AI-assisted understanding with geographic information to determine an appropriate response path.

### High-level flow

```text
User
 │
 ├── Location
 ├── Voice / Text
 └── Emergency Details
          │
          ▼
     Express API
          │
          ├──────────────► AI Classification
          │
          ├──────────────► Geographic Analysis
          │
          └──────────────► Responder Data
                            │
                            ▼
                  Response Coordination
                            │
              ┌─────────────┼─────────────┐
              ▼             ▼             ▼
         Incident       Responder      Emergency
         Category        Matching        Guidance
```

---

# ✨ Key Features

## 🆘 Emergency Reporting

Users can quickly submit an emergency incident along with relevant information and their current location.

---

## 📍 GPS-Based Location

The application can use the browser's geolocation capabilities to obtain the user's current coordinates.

Location information can then be used for:

* Incident mapping
* Proximity calculations
* Responder matching
* Emergency context

---

## 🤖 AI-Assisted Incident Classification

The application uses **Google Gemini** to process natural-language emergency descriptions.

The AI layer can help identify the nature of an incident and convert an unstructured report into structured information that the backend can work with.

Example:

```text
User report:

"There is a person trapped on the second floor.
The water is rising very quickly."

             ↓

AI Classification

Incident Type: Search & Rescue
Priority: High
Situation: Flooding
Required Response: Rescue assistance
```

The AI output is then combined with application logic rather than being treated as the sole source of truth.

---

## 🧠 Fallback Classification

The system includes a lightweight heuristic fallback mechanism for situations where the AI service is unavailable or cannot be used.

This allows the application to degrade gracefully instead of completely depending on an external AI service.

```text
Gemini Available?
      │
 ┌────┴────┐
 YES        NO
 │           │
 ▼           ▼
AI       Heuristic
Analysis  Fallback
 │           │
 └─────┬─────┘
       ▼
Incident Classification
```

---

## 🗺️ Disaster & Hazard Mapping

The application provides map-based visualization for relevant disaster information.

The mapping interface can be used to understand:

* Incident locations
* Hazard areas
* Shelters
* Relevant response locations

The project uses **Leaflet** for interactive maps.

---

## 🚑 Proximity-Based Responder Matching

After an incident is classified, the system can identify nearby responders based on geographic distance.

The prototype uses geographic coordinates and distance calculations to determine which available responder is closest to an incident.

Conceptually:

```text
Incident
   │
   ├── Responder A → 8.4 km
   ├── Responder B → 2.1 km
   ├── Responder C → 5.7 km
   │
   ▼
Nearest suitable responder
```

> The current implementation uses application-level/local responder data. It does not directly dispatch official emergency personnel.

---

## 🌐 Bilingual Emergency Guidance

The application is designed with accessibility in mind and provides emergency guidance suitable for users who may prefer English or Hindi.

The goal is to reduce the amount of technical knowledge required from someone who is already dealing with an emergency.

---

## 🎙️ Voice-Based Reporting

The browser's media capabilities can be used to capture emergency audio, allowing users to communicate without relying entirely on typing.

This is particularly useful when:

* The user is under stress
* Typing is inconvenient
* The situation requires quick reporting

---

## 🛟 Safety & First-Aid Guidance

The system can provide contextual emergency guidance based on the reported situation.

Examples include guidance related to:

* Flooding
* Fire
* Medical emergencies
* Immediate personal safety
* Evacuation

The guidance is intended as **general emergency assistance**, not as a replacement for professional emergency services.

---

# 🏗️ System Architecture

```text
                         ┌─────────────────────┐
                         │      Web Client     │
                         │                     │
                         │ SOS • GPS • Voice   │
                         │ Maps • Check-ins    │
                         └──────────┬──────────┘
                                    │
                                    ▼
                         ┌─────────────────────┐
                         │    Express Server   │
                         │                     │
                         │ API • Validation    │
                         │ Routing • Logic     │
                         └──────────┬──────────┘
                                    │
                  ┌─────────────────┼─────────────────┐
                  │                 │                 │
                  ▼                 ▼                 ▼
          ┌──────────────┐  ┌──────────────┐  ┌──────────────┐
          │ Google Gemini│  │ Geospatial   │  │ Local Data   │
          │      AI      │  │ Processing   │  │ Responders   │
          └──────────────┘  └──────────────┘  └──────────────┘
                  │                 │                 │
                  └─────────────────┼─────────────────┘
                                    ▼
                         ┌─────────────────────┐
                         │ Response Coordination│
                         │                     │
                         │ Classification     │
                         │ Matching           │
                         │ Guidance           │
                         └─────────────────────┘
```

---

# 🧠 Engineering Decisions

## Why Gemini?

Emergency reports are often unstructured.

A user might say:

> "Water has entered my house and my grandmother can't get downstairs."

Instead of forcing the user to fill out multiple forms, the AI layer can extract useful information from natural language.

---

## Why Geographic Distance?

Emergency response is inherently location-dependent.

The prototype therefore combines incident classification with geographic proximity instead of relying solely on the incident category.

---

## Why a Fallback Classifier?

An emergency-response system should avoid having a single external dependency become a complete point of failure.

The heuristic fallback provides basic classification capabilities when the AI service cannot be used.

---

## Why a Lightweight Frontend?

The prototype uses standard web technologies to keep the application lightweight and accessible through a browser.

This also provides direct access to browser capabilities such as:

* Geolocation
* Media recording
* Maps
* Device interaction

---

# 🛠️ Tech Stack

### Frontend

* HTML5
* CSS3
* JavaScript
* Leaflet
* Browser Geolocation API
* Browser Media APIs

### Backend

* Node.js
* Express.js

### AI

* Google Gemini API

### Mapping

* Leaflet
* OpenStreetMap-based map data

### Deployment

* Render

### Testing

* Node.js test scripts

---

# 📂 Project Structure

```text
hope-seeker-ai/
│
├── public/
│   ├── index.html
│   ├── app.js
│   └── styles.css
│
├── data/
│   └── application data
│
├── server.js
├── test-api.js
├── package.json
├── package-lock.json
├── .env.example
│
├── SECURITY.md
├── CONTRIBUTING.md
├── CODE_OF_CONDUCT.md
├── LICENSE
└── README.md
```

---

# ⚙️ Getting Started

## Prerequisites

Make sure you have:

* Node.js
* npm
* A Google Gemini API key

---

## 1. Clone the repository

```bash
git clone https://github.com/ujjwalraj-cds/hope-seeker-ai.git
```

```bash
cd hope-seeker-ai
```

---

## 2. Install dependencies

```bash
npm install
```

---

## 3. Configure environment variables

Create a `.env` file:

```env
GEMINI_API_KEY=your_gemini_api_key
PORT=3000
```

Never commit your actual API key to GitHub.

---

## 4. Start the server

```bash
npm start
```

The application should then be available at:

```text
http://localhost:3000
```

---

# 🧪 Testing

The project includes API-level tests for core functionality.

Run:

```bash
npm test
```

The tests cover areas such as:

* API availability
* Request handling
* Emergency payload processing
* Incident classification
* Responder matching
* Fallback behaviour

---

# 🔐 Security

Security is particularly important for an application dealing with emergency information.

Current security considerations include:

* Environment variables for API credentials
* `.env` excluded from version control
* Input validation
* Basic API error handling
* Security documentation

See:

**[SECURITY.md](SECURITY.md)**

for more information.

---

# ⚠️ Current Limitations

Hope Seeker AI is currently a **functional prototype/MVP**, not a production emergency-response system.

Important limitations include:

* Responder and shelter information may use local/simulated data.
* The application is not directly connected to official emergency dispatch infrastructure.
* Persistent production-grade database storage is not yet implemented.
* Authentication and role-based access are still areas for future development.
* Browser voice and geolocation features depend on device/browser permissions.
* AI responses depend on the availability and behaviour of the external AI service.
* The current deployment should not be relied upon as an official emergency service.

For an actual emergency, users should contact the appropriate official emergency services.

---

# 🗺️ Roadmap

## Phase 1 — Prototype

* [x] Emergency reporting
* [x] GPS location capture
* [x] AI-assisted classification
* [x] Fallback classification
* [x] Responder proximity matching
* [x] Disaster/hazard mapping
* [x] Voice-based reporting
* [x] Bilingual guidance
* [x] Web deployment

---

## Phase 2 — Reliability

* [ ] Persistent database
* [ ] User authentication
* [ ] Role-based access control
* [ ] Improved API validation
* [ ] Rate limiting
* [ ] Structured logging
* [ ] Better automated testing
* [ ] Monitoring and observability

---

## Phase 3 — Disaster Resilience

* [ ] Progressive Web App
* [ ] Service Worker caching
* [ ] Offline-first incident queue
* [ ] Background synchronization
* [ ] Local data persistence
* [ ] Experiment with offline/local AI models

---

## Phase 4 — Real-World Integration

* [ ] Verified emergency-service datasets
* [ ] Official API integrations where available
* [ ] Real responder accounts
* [ ] Coordinator/admin dashboard
* [ ] Push notification infrastructure
* [ ] SMS fallback
* [ ] Advanced geospatial routing

---

# 🔬 Future Research

Several areas require further research before the system could be considered for real-world disaster-response usage.

### AI Reliability

Emergency classification needs to be evaluated against real-world disaster scenarios and noisy, incomplete user reports.

### False Positives & False Negatives

Incorrect classification could have serious consequences, so the system would require carefully designed evaluation datasets and human oversight.

### Geospatial Routing

Simple geographic distance is not equivalent to actual travel time.

Future versions could consider:

* Roads
* Flooded areas
* Blocked routes
* Traffic
* Terrain
* Vehicle accessibility

### Connectivity

Disasters can damage communication infrastructure.

Future versions will investigate:

* Offline-first architecture
* Store-and-forward communication
* Local caching
* Background synchronization
* Alternative communication channels

### Privacy

Location and emergency information can be sensitive.

A production implementation would require stronger privacy controls, data minimization, access controls, retention policies, and secure storage.

---

# 📊 Example Incident Flow

```text
User reports:

"There's a fire in the building and
two people are still inside."

                ↓

        AI Classification

        Type: Fire
        Priority: Critical
        Requirement: Rescue

                ↓

        GPS Coordinates

                ↓

     Nearby Responder Search

                ↓

       Candidate Responders

                ↓

       Response Coordination

                ↓

      Emergency Safety Guidance
```

---

# 🎯 Project Goals

Hope Seeker AI is being developed around five core principles:

### 1. Speed

Reduce the time required to communicate an emergency.

### 2. Simplicity

Make reporting possible even when the user is under stress.

### 3. Intelligence

Use AI to transform unstructured descriptions into useful information.

### 4. Location Awareness

Use geographic context to improve response coordination.

### 5. Resilience

Design the system so that individual components can fail without completely stopping the workflow.

---

# 📈 What I Am Building Toward

The current deployment is the **first working version**, not the final product.

The long-term goal is to evolve Hope Seeker AI from a demonstration into a more robust disaster-coordination platform with:

```text
                    ┌───────────────────────┐
                    │    Citizen Reports    │
                    └───────────┬───────────┘
                                │
                                ▼
                    ┌───────────────────────┐
                    │ AI Incident Analysis  │
                    └───────────┬───────────┘
                                │
                                ▼
                    ┌───────────────────────┐
                    │ Response Coordination │
                    └───────────┬───────────┘
                                │
              ┌─────────────────┼─────────────────┐
              ▼                 ▼                 ▼
        Volunteers         Coordinators      Authorities
              │                 │                 │
              └─────────────────┼─────────────────┘
                                ▼
                    ┌───────────────────────┐
                    │    Faster Response   │
                    └───────────────────────┘
```

---

# 🤝 Contributing

Contributions, suggestions, and ideas are welcome.

If you would like to contribute:

1. Fork the repository.
2. Create a feature branch.
3. Make your changes.
4. Test the changes.
5. Open a pull request.

Please read **[CONTRIBUTING.md](CONTRIBUTING.md)** before contributing.

---

# 📄 License

This project is licensed under the **MIT License**.

See [LICENSE](LICENSE) for details.

---

# 👨‍💻 Author

**Ujjawal Raj**

Computer Science / AI enthusiast building practical software projects around **AI, web development, and real-world problem solving**.

### Project

**Hope Seeker AI**

🚀 [Live Demo](https://hope-seeker-ai.onrender.com)

💻 [GitHub Repository](https://github.com/ujjwalraj-cds/hope-seeker-ai)

---

## ⭐ Support the Project

If you find Hope Seeker AI interesting, consider giving the repository a ⭐ on GitHub.

The project is actively evolving, and feedback on the architecture, AI pipeline, disaster-response workflow, and future improvements is welcome.
