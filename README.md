# 🌱 AgriAssist — Premium AI-Powered Agricultural Intelligence System

AgriAssist is a state-of-the-art, web-based platform designed to provide farmers, researchers, and enthusiasts with instant access to agricultural advice, real-time weather alerts, commodity market prices, and a supportive community.

Built using **React**, **Vite**, **TypeScript**, **Node.js/Express**, **Supabase**, and powered by **Google Gemini AI**.

---

## 🚀 Key Features & Architecture

* **🤖 Multimodal AI Assistant (Gemini)**: An intelligent agricultural bot capable of processing text queries, analyzing uploaded leaf/crop images for disease detection, and transcribing speech-to-text (STT) queries directly from web browsers.
* **🔐 Passkey & Biometric Authentication**: Modern, passwordless authentication using TouchID, FaceID, or Windows Hello. Integrated with `@simplewebauthn` and Supabase magic links for seamless, secure user profiles.
* **☁️ Weather Forecasting & Alerts**: Live weather updates tailored to the user's location with automated alert triggers for adverse climatic conditions (squalls, storms, tornadoes) to help plan farming activities.
* **🌾 Real-Time Community Forum & Chatrooms**: Group discussion rooms and community forum posts with instant, real-time database updates powered by Supabase real-time channels.
* **📈 Cache-Based Market Prices**: Direct access to local agricultural commodity pricing, fetched securely and optimized using a cached database storage layer.
* **🛡️ Secure Backend Proxy (Advisory)**: Moves sensitive crop advisory prompts and Gemini API invocations to secure Node.js server routes and Vercel serverless functions to avoid client-side API key leakage.

---

## 🗺️ System Design & Workflow

```
                        [ User Login Page ]
                          /            \
                 (Passwordless)     (Email & Password)
                     /                      \
            [Passkey Auth / WebAuthn]     [Supabase Auth]
                   \                        /
                    v                      v
                [ -------- Dashboard Hub -------- ]
                /           |            |        \
               /            |            |         \
              v             v            v          v
       [Weather API]  [Market Prices] [Community] [AI Assistant]
             |              |            |          /    |    \
      (Severe Alerts) (Edge Cached) (Real-Time)  (Text) (STT) (Vision)
```

---

## 🛠️ Tech Stack

* **Frontend Client**: React (v18), Vite, TypeScript, Tailwind CSS, shadcn/ui, React Router, Lucide Icons, Recharts (for visualization)
* **Backend API Server**: Node.js, Express, `tsx` (TypeScript runtime runner)
* **Serverless Functions**: Vercel Serverless Functions (located in `api/`) for production API endpoints
* **Database & BaaS**: Supabase (PostgreSQL, Storage buckets for crop images, Edge Functions, real-time channels)
* **AI/LLM Engine**: Google Gemini API (`gemini-2.5-flash`), Speech-to-Text via base64 inline audio data
* **Authentication**: WebAuthn (`@simplewebauthn/server` & `@simplewebauthn/browser`), JWT, Supabase Admin Magic Links
* **External APIs**: OpenWeatherMap API

---

## ⚙️ Quick Start

### 1. Prerequisites
- **Node.js** (v18+ installed)
- **Supabase CLI** (for managing backend edge functions/migrations)
- **Gemini API Key** (Get yours from [Google AI Studio](https://aistudio.google.com/apikey))
- **OpenWeatherMap API Key** (Get yours from [OpenWeatherMap](https://openweathermap.org/api) for live weather features)

### 2. Installation
Clone the repository and install root dependencies:
```bash
# Clone the repository
git clone <YOUR_GIT_URL>
cd agriassist

# Install dependencies
npm install
```

### 3. Environment Setup
Create a `.env` file in the root directory:
```bash
touch .env
```
Populate `.env` with the following variables:
```env
# Supabase Configuration (Get from Supabase Settings -> API)
VITE_SUPABASE_URL="https://your-project-id.supabase.co"
VITE_SUPABASE_PUBLISHABLE_KEY="your-anon-key"
SUPABASE_SERVICE_ROLE_KEY="your-service-role-key"

# AI & Weather API Keys
GEMINI_API_KEY="your-gemini-api-key"
OPENWEATHERMAP_API_KEY="your-openweathermap-api-key"
HUGGINGFACE_API_KEY="your-huggingface-api-key"  # Optional, for speech-to-text
```

### 4. Database Setup
Ensure migrations are pushed to your Supabase instance:
```bash
# Link your local repository to your Supabase project
npx supabase link --project-ref <YOUR_PROJECT_ID>

# Apply local migrations to the database
npx supabase db push
```

### 5. Running the Application
Start the frontend development server and the unified Node.js API server concurrently:
```bash
npm start
```
The application will be available at **[http://localhost:8080](http://localhost:8080)**, proxying API requests to port `3000`.

---
Developed by Sanjay Kumar
