<<<<<<< HEAD
# Deployment and DevOps for MERN Applications

This assignment focuses on deploying a full MERN stack application to production, implementing CI/CD pipelines, and setting up monitoring for your application.
=======
# Chumbi Nyiri

🚀 **Production-ready** full-stack real-time chat application built with the MERN stack. Features secure authentication, real-time messaging via Socket.IO, and a beautiful modern UI.
>>>>>>> 877ece3 (chumbi nyiri)

## ✨ Highlights

<<<<<<< HEAD
You will:
1. Prepare your MERN application for production deployment
2. Deploy the backend to a cloud platform
3. Deploy the frontend to a static hosting service
4. Set up CI/CD pipelines with GitHub Actions
5. Implement monitoring and maintenance strategies
=======
- 🔐 **Secure Authentication** - Clerk-backed JWT authentication with automatic profile sync
- 💬 **Real-Time Messaging** - Socket.IO integration for instant message delivery
- 🎨 **Modern UI** - Beautiful dark theme with Tailwind CSS and smooth animations
- 📱 **Responsive Design** - Works seamlessly on desktop and mobile devices
- 🔄 **Live Updates** - Conversations and messages update in real-time across all devices
- 🏗️ **Production Ready** - No console logs, proper error handling, comprehensive documentation
- 🚀 **Scalable Architecture** - Ready for horizontal scaling with Redis adapter support
- 📊 **MongoDB** - Efficient data persistence with proper indexing

## Project Structure

```
.
├── backend            # Express + MongoDB API
└── frontend           # Vite + React client
```
>>>>>>> 877ece3 (chumbi nyiri)

## Prerequisites

<<<<<<< HEAD
1. Accept the GitHub Classroom assignment invitation
2. Clone your personal repository that was created by GitHub Classroom
3. Follow the setup instructions in the `Week7-Assignment.md` file
4. Use the provided templates and configuration files as a starting point
=======
- Node.js 18+ and npm
- MongoDB instance (local or hosted)
- Clerk application with JWT template configured (or integration fallback)
>>>>>>> 877ece3 (chumbi nyiri)

## Backend Environment

<<<<<<< HEAD
- `Week7-Assignment.md`: Detailed assignment instructions
- `.github/workflows/`: GitHub Actions workflow templates
- `deployment/`: Deployment configuration files and scripts
- `.env.example`: Example environment variable templates
- `monitoring/`: Monitoring configuration examples
=======
Create `backend/.env` with the following keys:
>>>>>>> 877ece3 (chumbi nyiri)

| Variable | Description | Example |
| --- | --- | --- |
| `PORT` | API port (defaults to 5000) | `5000` |
| `MONGODB_URI` | MongoDB connection string | `mongodb://127.0.0.1:27017/meridian-chat` |
| `CLERK_SECRET_KEY` | Clerk secret key for server-side verification | `sk_test_...` |
| `CLERK_PUBLISHABLE_KEY` | Clerk publishable key (used to seed profile data) | `pk_test_...` |
| `CLERK_JWT_TEMPLATE` | (Optional) custom JWT template name | `integration_fallback` |
| `ALLOWED_ORIGINS` | Comma-separated list of allowed front-end origins | `http://localhost:5173` |

<<<<<<< HEAD
- A completed MERN stack application from previous weeks
- Accounts on the following services:
  - GitHub
  - MongoDB Atlas
  - Render, Railway, or Heroku (for backend)
  - Vercel, Netlify, or GitHub Pages (for frontend)
- Basic understanding of CI/CD concepts

## Deployment Platforms

### Backend Deployment Options
- **Render**: Easy to use, free tier available
- **Railway**: Developer-friendly, generous free tier
- **Heroku**: Well-established, extensive documentation

### Frontend Deployment Options
- **Vercel**: Optimized for React apps, easy integration
- **Netlify**: Great for static sites, good CI/CD
- **GitHub Pages**: Free, integrated with GitHub

## CI/CD Pipeline

The assignment includes templates for setting up GitHub Actions workflows:
- `frontend-ci.yml`: Tests and builds the React application
- `backend-ci.yml`: Tests the Express.js backend
- `frontend-cd.yml`: Deploys the frontend to your chosen platform
- `backend-cd.yml`: Deploys the backend to your chosen platform
=======
> `ALLOWED_ORIGINS` is applied to both Express CORS and Socket.IO. If unset, the server allows `http://localhost:5173` and `http://127.0.0.1:5173`.
>>>>>>> 877ece3 (chumbi nyiri)

## Frontend Environment

Create `frontend/.env` with:

<<<<<<< HEAD
1. Complete all deployment tasks
2. Set up CI/CD pipelines with GitHub Actions
3. Deploy both frontend and backend to production
4. Document your deployment process in the README.md
5. Include screenshots of your CI/CD pipeline in action
6. Add URLs to your deployed applications
=======
| Variable | Description | Example |
| --- | --- | --- |
| `VITE_CLERK_PUBLISHABLE_KEY` | Clerk publishable key | `pk_test_...` |
| `VITE_CLERK_JWT_TEMPLATE` | (Optional) template request name | `integration_fallback` |
| `VITE_API_URL` | Backend base URL | `http://localhost:5000` |
| `VITE_SOCKET_URL` | Socket.IO server URL (defaults to `VITE_API_URL`) | `http://localhost:5000` |
>>>>>>> 877ece3 (chumbi nyiri)

## Installation

```bash
# install backend dependencies
cd backend
npm install

# install frontend dependencies
cd ../frontend
npm install
```

## Running Locally

```bash
# terminal 1 - backend API + socket server
cd backend
npm run dev

# terminal 2 - frontend (Vite dev server)
cd frontend
npm run dev
```

The API listens on `http://localhost:5000` (unless you override `PORT`). The Vite dev server runs on `http://localhost:5173` by default.

### Available Scripts

Backend (`backend`):

- `npm run dev` – start API with Nodemon
- `npm start` – start API without reload

Frontend (`frontend`):

- `npm run dev` – Vite development server
- `npm run build` – production bundle
- `npm run preview` – preview production build
- `npm run lint` – run ESLint

## API Overview

All endpoints require a valid Clerk JWT (Bearer token).

- `GET /api/users` – list user directory profiles
- `POST /api/users/sync` – upsert the authenticated user's profile
- `GET /api/conversations` – list conversations that include the current user
- `POST /api/conversations` – ensure a one-to-one conversation exists
- `GET /api/conversations/:conversationId` – fetch conversation detail
- `GET /api/messages/:conversationId` – fetch message history
- `POST /api/messages` – send a message to a conversation

Health endpoints:

- `GET /` – simple readiness string
- `GET /healthz` – health check payload

## Socket Events

Clients authenticate the WebSocket connection with the same Clerk JWT (sent via `auth.token`).

- `conversation:join` – join a conversation room
- `conversation:leave` – leave a conversation room
- `message:new` – emit a new message; echoed to conversation members
- `conversation:update` – emitted when unread counts change

## Data Models

- `Conversation` – members, last message metadata, unread counts (Map keyed by Clerk ID)
- `Message` – conversation reference, sender info, text, read receipts, status
- `UserProfile` – cached Clerk profile fields for faster display

`backend/src/models` contains the full schema definitions.

## Clerk Notes

- API guards and Socket.IO middleware verify JWTs via `@clerk/backend`.
- Set `CLERK_JWT_TEMPLATE` / `VITE_CLERK_JWT_TEMPLATE` if you use a custom template; otherwise the integration fallback is used.
- Ensure the template includes the `sub`, `sid`, `email`, and image claims for profile sync.

## 📚 Documentation

This project includes comprehensive documentation:

- **[ENVIRONMENT_SETUP.md](./ENVIRONMENT_SETUP.md)** - Complete guide to environment configuration
- **[DEPLOYMENT_GUIDE.md](./DEPLOYMENT_GUIDE.md)** - Step-by-step deployment instructions
- **[TESTING_GUIDE.md](./TESTING_GUIDE.md)** - Testing procedures and verification
- **[FEATURE_VERIFICATION.md](./FEATURE_VERIFICATION.md)** - Complete feature checklist

## 🎯 Key Features

### User Management
- User authentication via Clerk
- Automatic profile synchronization
- User directory with search
- Avatar and display name support

### Conversations
- One-to-one conversations
- Real-time conversation list updates
- Last message preview
- Unread message counts
- Timestamp formatting

### Messaging
- Send and receive messages in real-time
- Message history persistence
- Read receipts and status indicators
- Auto-scroll to new messages
- Message timestamps

### Real-Time Features
- Socket.IO WebSocket connections
- Instant message delivery
- Live conversation updates
- User presence tracking
- Automatic reconnection

### User Experience
- Modern dark theme UI
- Responsive design (mobile-friendly)
- Loading and empty states
- Error handling with user-friendly messages
- Smooth animations

## 🔧 Technology Stack

### Backend
- **Node.js** - Runtime environment
- **Express.js** - Web framework
- **MongoDB** - Database
- **Mongoose** - ODM for MongoDB
- **Socket.IO** - Real-time communication
- **Clerk** - Authentication

### Frontend
- **React 19** - UI library
- **Vite** - Build tool
- **Tailwind CSS** - Styling
- **Socket.IO Client** - WebSocket client
- **Axios** - HTTP client
- **Clerk React** - Authentication

## 🚀 Quick Start

### Prerequisites
- Node.js 18+
- MongoDB (local or Atlas)
- Clerk account

### Installation

```bash
# Clone the repository
git clone https://github.com/PLP-MERN-Stack-Development/Week5-Chat
cd Week5-Chat

# Install backend dependencies
cd backend
npm install

# Install frontend dependencies
cd ../frontend
npm install
```

### Configuration

See [ENVIRONMENT_SETUP.md](./ENVIRONMENT_SETUP.md) for detailed configuration instructions.

### Running

```bash
# Terminal 1 - Backend
cd backend
npm run dev

# Terminal 2 - Frontend
cd frontend
npm run dev
```

Visit `http://localhost:5173` to use the application.

## 🧪 Testing

See [TESTING_GUIDE.md](./TESTING_GUIDE.md) for comprehensive testing procedures.

Quick verification:
```bash
# Test backend health
curl http://localhost:5000/healthz

# Expected response
{"status":"ok"}
```

## 📦 Production Deployment

See [DEPLOYMENT_GUIDE.md](./DEPLOYMENT_GUIDE.md) for detailed deployment instructions.

### Quick Deploy Options
- **Backend**: Heroku, Railway, AWS EC2
- **Frontend**: Vercel, Netlify, AWS S3 + CloudFront
- **Database**: MongoDB Atlas

## 🛡️ Security Features

- JWT-based authentication
- Server-side token verification
- CORS protection
- Input validation
- XSS prevention
- Secure WebSocket connections
- Environment-based configuration
- No sensitive data in client code

## 📈 Performance

- Database indexing for fast queries
- Efficient Socket.IO room management
- React component memoization
- Optimized re-renders
- Connection pooling
- Lazy loading

## 🤝 Contributing

Contributions are welcome! Please follow these guidelines:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the ISC License.

## 🙏 Acknowledgments

- PLP MERN Stack Development Program
- Clerk for authentication services
- MongoDB for database services
- Socket.IO team for real-time capabilities

## 📞 Support

For issues and questions:
- Check [TESTING_GUIDE.md](./TESTING_GUIDE.md) troubleshooting section
- Review [ENVIRONMENT_SETUP.md](./ENVIRONMENT_SETUP.md) for configuration help
- Open an issue on GitHub

## 🎓 Learning Resources

<<<<<<< HEAD
- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [MongoDB Atlas Documentation](https://docs.atlas.mongodb.com/)
- [Render Documentation](https://render.com/docs)
- [Railway Documentation](https://docs.railway.app/)
- [Vercel Documentation](https://vercel.com/docs)
- [Netlify Documentation](https://docs.netlify.com/) 
=======
- [Express.js Documentation](https://expressjs.com/)
- [React Documentation](https://react.dev/)
- [MongoDB Documentation](https://docs.mongodb.com/)
- [Socket.IO Documentation](https://socket.io/docs/)
- [Clerk Documentation](https://clerk.com/docs)

---

**Status**: Production Ready ✅  
**Version**: 1.0.0  
**Last Updated**: November 7, 2025

Repository: https://github.com/PLP-MERN-Stack-Development/Week5-Chat

>>>>>>> 877ece3 (chumbi nyiri)
