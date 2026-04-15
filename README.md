<div align="center">

# BlinkBet

**A real-time 1v1 competitive gaming platform where two players compete in a live staring contest powered by AI-driven eye-tracking.**

> *Two Players • One Live Stream • First to Blink Loses • Real-Time Gameplay*

[![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![React](https://img.shields.io/badge/React_19-61DAFB?style=flat-square&logo=react&logoColor=black)](https://react.dev/)
[![WebRTC](https://img.shields.io/badge/WebRTC_P2P-333?style=flat-square&logo=webrtc&logoColor=white)](https://webrtc.org/)
[![MediaPipe](https://img.shields.io/badge/MediaPipe_Vision-4285F4?style=flat-square&logo=google&logoColor=white)](https://developers.google.com/mediapipe)
[![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat-square&logo=node.js&logoColor=white)](https://nodejs.org/)
[![Status](https://img.shields.io/badge/Status-Production_Ready-brightgreen?style=flat-square)]()

<img width="1189" height="655" alt="BlinkBet Landing" src="https://github.com/user-attachments/assets/66379a4b-6220-4409-b2d7-9857f26eec50" />

</div>

---

## 🎮 Project Overview

**BlinkBet** is a full-stack, real-time gaming platform that combines **peer-to-peer video streaming**, **AI-powered eye-tracking**, and **live player interaction** to create an engaging, low-latency multiplayer experience.

**Core Concept:** Players are randomly matched, establish a peer-to-peer video connection, and compete in a blink-detection game where the first person to blink loses. Blink detection runs entirely **client-side using MediaPipe** (no server sees your face), ensuring complete privacy.

This project demonstrates advanced full-stack competencies including **real-time communication**, **computer vision/AI integration**, **peer-to-peer networking**, and **production-grade web architecture**.

---

## ✨ Key Features

### 🎯 Core Gameplay
- **Real-time 1v1 Matchmaking:** Random peer pairing via WebSocket with instant connection
- **P2P Video Streaming:** Leverages WebRTC for media delivery — zero server media overhead
- **Live In-Game Chat:** WebSocket-synced text communication during matches
- **Instant Match Results:** Real-time outcome determination with match statistics

### 👁️ Computer Vision
- **Client-Side Blink Detection:** MediaPipe Face Landmark Detection extracts facial geometry every frame
- **Eye Aspect Ratio (EAR) Algorithm:** Proprietary thresholds calibrated for accuracy
- **Privacy-First Design:** Facial data never leaves the player's browser
- **Low-Latency Processing:** 30+ FPS blink detection on consumer hardware

### 🔧 Technical Excellence
- **TypeScript Everywhere:** 100% type-safe frontend and backend
- **Modern React 19:** Functional components with hooks, optimized rendering
- **Responsive UI:** Tailwind CSS for mobile-first design
- **High-Performance Networking:** WebSocket for real-time sync, WebRTC for media

---

## 🏗️ Architecture

### System Flow

```
┌──────────────┐                    ┌──────────────┐
│   Player A   │                    │   Player B   │
└──────┬───────┘                    └───────┬──────┘
       │                                   │
       └───────────┬─────────────────────┬─┘
                   │   WebSocket         │
              ┌────▼──────────────────┐ │
              │  Signaling Server     │ │
              │  • Room Pairing       │─┘
              │  • SDP/ICE Relay      │
              │  • Match Events       │
              └───────────────────────┘
       
       ┌─────────────────────────────────┐
       │   Peer-to-Peer Connection       │
       │   • MediaStream (Video/Audio)   │
       │   • Direct Data Channel         │
       │   • No Media Server             │
       └─────────────────────────────────┘
       
       ┌─────────────────────────────────┐
       │   MediaPipe Face Detection      │
       │   • Blink Recognition           │
       │   • Client-Side Processing      │
       └─────────────────────────────────┘
```

### Technology Stack

| Layer | Technology | Purpose |
|---|---|---|
| **Frontend Framework** | React 19 + Vite + TypeScript | High-performance UI with HMR |
| **Styling** | Tailwind CSS | Responsive, utility-first design |
| **Authentication** | Google OAuth 2.0 | Frictionless user login |
| **Real-Time Comms** | WebRTC | P2P media streaming (low latency) |
| **Signaling** | WebSocket (`ws` library) | SDP/ICE exchange, matchmaking, match events |
| **Computer Vision** | MediaPipe Face Landmark | Client-side blink detection |
| **Backend** | Node.js + TypeScript | Stateless signaling server |

---

## 📁 Project Structure

```
BlinkBet/
│
├── 📂 frontend/                    # React + Vite SPA
│   ├── src/
│   │   ├── App.tsx                 # Route definitions & app shell
│   │   ├── main.tsx                # React root, auth context
│   │   ├── pages/
│   │   │   ├── random.tsx          # Gameplay screen (video, chat, results)
│   │   │   └── initProcess.tsx     # Match setup & WebSocket handlers
│   │   ├── components/
│   │   │   └── faceDetection.tsx   # MediaPipe integration & EAR detection
│   │   ├── styles/
│   │   │   └── tailwind.css        # Global Tailwind directives
│   │   └── utils/
│   │       └── webrtcConfig.ts     # STUN/TURN servers, peer connection setup
│   ├── .env                        # Google Client ID, server URL
│   └── package.json
│
└── 📂 backend/                     # Node.js WebSocket Server
    ├── src/
    │   ├── index.ts                # Main server file
    │   ├── roomManager.ts          # Room pairing & state
    │   ├── signaling.ts            # SDP/ICE relay
    │   └── eventEmitter.ts         # Match lifecycle events
    ├── .env                        # Server port, allowed origins
    └── package.json
```

---

## 🚀 Getting Started

### Prerequisites

Before you begin, ensure you have:

- **Node.js 18+** — [Download](https://nodejs.org/)
- **Git** — [Install](https://git-scm.com/)
- **A modern web browser** with camera/microphone access

### Environment Setup

#### 1. Create Google OAuth Credentials
1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Create a new OAuth 2.0 credential (type: Web application)
3. Add `http://localhost:5173` to authorized JavaScript origins
4. Copy your **Client ID**

### Frontend Installation

```bash
cd frontend
npm install
```

Create `frontend/.env`:
```env
VITE_GOOGLE_CLIENT_ID=your_google_oauth_client_id_here
VITE_SIGNALING_SERVER_URL=ws://localhost:8080
```

Start the dev server:
```bash
npm run dev
```
> Runs on `http://localhost:5173`

### Backend Installation

```bash
cd backend
npm install
```

Create `backend/.env`:
```env
PORT=8080
ALLOWED_ORIGINS=http://localhost:5173
NODE_ENV=development
```

Start the signaling server:
```bash
npm run dev
```
> Runs on `ws://localhost:8080`

### Running Locally (Full Stack)

1. **Terminal 1:** Backend signaling server
   ```bash
   cd backend && npm run dev
   ```

2. **Terminal 2:** Frontend dev server
   ```bash
   cd frontend && npm run dev
   ```

3. Open `http://localhost:5173` in **two separate browser windows/tabs** and test matchmaking
   - Allow camera/microphone permissions when prompted
   - Both players should be connected to the same signaling server

---

## 🎯 How It Works: Detailed Flow

### Phase 1: Authentication
- User clicks "Sign In with Google"
- OAuth consent screen → ID token issued
- User is logged in and ready to play

### Phase 2: Matchmaking & WebRTC Handshake
1. **Room Request:** Frontend opens WebSocket → sends room join message
2. **Pairing:** Backend pairs two waiting players into a unique room
3. **SDP Offer:** Player A's browser creates WebRTC offer, sends via WebSocket
4. **SDP Answer:** Player B receives offer, creates answer, sends back
5. **ICE Candidates:** Both clients exchange STUN/TURN server candidates
6. **P2P Established:** Once connection succeeds, direct video/audio stream flows between peers

### Phase 3: Game Start
- Video and audio streams active on both ends
- In-game chat ready for communication
- Both players see each other live

### Phase 4: Blink Detection & Game
1. **MediaPipe Initialization:** Face Landmark model loads in both browsers
2. **Frame Processing:** Every 30ms, facial landmarks extracted
3. **EAR Calculation:** Eye Aspect Ratio = `(||p2-p6|| + ||p3-p5||) / (2 * ||p1-p4||)`
4. **Threshold Logic:** If EAR < 0.15 for >3 consecutive frames → **Blink Detected**
5. **Event Broadcast:** Winner determined, confetti/victory screen shown
6. **Match Result:** Winner displayed to both players with match statistics

---

## 🧠 Technical Highlights

### Eye Aspect Ratio (EAR) Algorithm
```
EAR = (distance(eye_top, eye_bottom) + distance(eye_inner, eye_outer)) / (2 * distance(eye_corner_left, eye_corner_right))

Threshold: 0.15 (empirically tuned)
Hold Duration: 3+ frames to confirm blink (reduces false positives)
Sample Rate: 30 FPS for real-time detection
```

### Privacy & Security
- ✅ **Client-Side Processing:** No facial data sent to servers
- ✅ **Peer-to-Peer:** No media server observes video streams
- ✅ **Type-Safe:** 100% TypeScript ensures reliability
- ✅ **Open Source:** Full transparency on GitHub

---

## 📚 Learning Resources

- [MediaPipe Face Landmark Docs](https://developers.google.com/mediapipe/solutions/vision/face_landmarker)
- [WebRTC for Beginners](https://www.html5rocks.com/en/tutorials/webrtc/basics/)
- [React 19 Documentation](https://react.dev/)
- [Tailwind CSS Utility-First](https://tailwindcss.com/docs)
- [Node.js WebSocket Guide](https://nodejs.org/en/docs/)

---

## 🤝 Contributing

Contributions are welcome! Please follow these guidelines:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/your-feature`)
3. Commit with clear messages (`git commit -m "Add feature X"`)
4. Push to your branch (`git push origin feature/your-feature`)
5. Open a pull request with a detailed description

---

## 📄 License

This project is licensed under the **MIT License** — see the [LICENSE](./LICENSE) file for details.

---

## 💡 About the Creator

Built by **Harsh Yadav** — a passionate full-stack developer with expertise in Web3, real-time systems, and competitive programming.

- 🔗 [GitHub](https://github.com/Harshyadav0987)
- 💼 [LinkedIn](https://www.linkedin.com/in/harsh-yadav-783917299/)
- 🎯 [LeetCode](https://leetcode.com/u/harshbelike/)

---

<div align="center">

### ⭐ If you find this project interesting, please consider starring it on GitHub!

**Made with ❤️ using TypeScript, React, Solana, and WebRTC**

</div>
