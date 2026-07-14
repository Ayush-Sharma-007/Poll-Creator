# Poll Creator

A real-time polling application where hosts create live "rooms," broadcast questions to participants, and see responses update instantly — built with the MERN stack and Socket.io.

## Features

- **User Authentication** — Signup/login with JWT-based token authentication
- **Live Poll Rooms** — Hosts create rooms; participants join via a shareable link or QR code
- **Real-Time Question Broadcasting** — Hosts push questions to all connected participants instantly via WebSockets (Socket.io)
- **Live Response Aggregation** — Poll submissions are broadcast back to the host in real time as participants respond
- **Word Cloud Visualization** — Open-ended responses are rendered as a word cloud for quick visual insight
- **QR Code Join** — Each room generates a QR code so participants can join instantly from mobile
- **Room Management Dashboard** — Hosts can create, view, and manage their rooms

## Tech Stack

**Frontend**
- Next.js (React framework, App Router)
- Tailwind CSS
- Axios (API requests)
- Formik + Yup (form handling & validation)
- Socket.io-client (real-time communication)
- react-qr-code, react-wordcloud

**Backend**
- Node.js + Express
- MongoDB with Mongoose (data modeling for users and rooms)
- Socket.io (WebSocket server for real-time events)
- JSON Web Tokens (authentication)
- CORS-enabled REST API

## How It Works

- Users sign up and log in through a REST API; on successful login the backend issues a JWT used to authenticate subsequent requests
- A host creates a "room" (stored in MongoDB, linked to the owning user) and shares it via link or generated QR code
- Participants join the room, which opens a Socket.io connection scoped to that room's ID
- When the host sets a question, it's emitted over the socket to everyone in that room in real time — no polling or page refresh needed
- As participants submit answers, responses are emitted back to the host's socket and rendered live, with open-text answers visualized as a word cloud

## Project Structure

```
Poll-Creator/
├── Backend/
│   ├── index.js          # Express + Socket.io server entry point
│   ├── connection.js      # MongoDB connection setup
│   ├── models/            # Mongoose schemas (User, Room)
│   └── routers/           # REST endpoints (auth, room CRUD)
└── frontend/
    └── src/
        ├── app/            # Next.js pages (login, signup, host, poll, manage-room)
        └── components/     # Shared UI components
```

## Getting Started

**Backend**
```bash
cd Backend
npm install
# create a .env file with MONGO_URI and JWT_SECRET
npm run dev
```

**Frontend**
```bash
cd frontend
npm install
npm run dev
```

## Possible Future Improvements

- Add password hashing (bcrypt) if not already applied on the backend
- Support multiple question types (multiple choice, rating scale, not just open text)
- Add poll result export (CSV/PDF)
- Deploy backend with persistent WebSocket support (Render/Railway) and frontend on Vercel

## Author

Ayush Sharma
