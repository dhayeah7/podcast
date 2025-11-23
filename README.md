# 🎙️ AI Podcast Clipper SaaS
Automatically turn long podcast videos into viral short-form clips.

This platform uses AI to convert long-form podcast videos into short, engaging vertical clips for **YouTube Shorts**, **TikTok**, and **Instagram Reels**.  
Everything—transcription, highlight detection, speaker tracking, subtitles, and rendering—is fully automated.

---

## 📺 Live Demo

👉 **https://ai-podcast-clipper-frontend-khaki.vercel.app/signup**

---

## ✨ Features

| Feature | Technology |
|--------|------------|
| **Transcription** | WhisperX (FastAPI + Modal GPU) |
| **Viral Clip Detection** | Google Gemini 2.5 Pro |
| **Speaker Detection** | LR-ASD model |
| **Vertical Clip Rendering** | FFMPEGCV + OpenCV |
| **Styled Subtitles** | ASS subtitle styling |
| **Authentication** | Auth.js (NextAuth) |
| **Background Jobs** | Inngest |
| **File Storage** | AWS S3 |
| **Dashboard** | Next.js 15 + Tailwind + Shadcn UI |

---

## ⚙️ How It Works

1. User uploads a video → saved to **AWS S3**.
2. An **Inngest** event starts processing.
3. **Modal backend**:
   - Transcribes audio with WhisperX  
   - Detects viral timestamps with Gemini  
   - Identifies active speakers  
   - Crops & renders vertical clips with subtitles  
4. Final clips are uploaded back to S3 and shown in the dashboard.

---

## 🧱 Tech Stack

| Layer | Tools |
|-------|-------|
| Frontend | Next.js 15, TypeScript, Tailwind, Shadcn |
| Backend | FastAPI (Python) on Modal |
| Queueing | Inngest |
| AI Models | WhisperX, Gemini, LR-ASD |
| Video Processing | FFMPEG, OpenCV |
| Auth | Auth.js |
| Storage | AWS S3 |

---

## 🛠 Local Development Setup

### 1. Clone Project
```bash
git clone https://github.com/dhayeah/podcast.git
```

### 2. Backend Setup (Modal + FastAPI)
```bash
cd ai-podcast-clipper-backend
pip install -r requirements.txt
git clone https://github.com/Junhua-Liao/LR-ASD.git asd
```

Run using Modal:
```bash
modal setup
modal run main.py
modal deploy main.py
```

### 3. Frontend Setup (Next.js)
```bash
cd ai-podcast-clipper-frontend
npm install
npm run dev
npm run inngest-dev
```

---

## 🔐 Environment Variables

### Frontend (Vercel)
```
NEXT_PUBLIC_AWS_REGION=
NEXT_PUBLIC_S3_BUCKET=
AUTH_SECRET=
NEXTAUTH_URL=
INNGEST_EVENT_KEY=
```

### Backend (Modal)
```
AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
S3_BUCKET_NAME=
GEMINI_API_KEY=
MODAL_TOKEN_SECRET=
```

---

## ☁️ AWS S3 Configuration

### CORS
```json
[
  {
    "AllowedHeaders": ["*"],
    "AllowedMethods": ["PUT"],
    "AllowedOrigins": ["*"],
    "ExposeHeaders": ["ETag"]
  }
]
```

### IAM Policy
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Action": ["s3:ListBucket"],
      "Effect": "Allow",
      "Resource": "arn:aws:s3:::your-bucket-name"
    },
    {
      "Action": ["s3:GetObject", "s3:PutObject"],
      "Effect": "Allow",
      "Resource": "arn:aws:s3:::your-bucket-name/*"
    }
  ]
}
```

---

## 👨‍💻 Author
**Dhayanandhan M**

---

## 📄 License
MIT License – free for personal and commercial use.
