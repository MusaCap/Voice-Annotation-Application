# Product Requirements Document (PRD)
## Voice Annotation Application (Human-in-the-Loop Correction System)

---

## 1. Overview

### Purpose
To build a web-based application that:
- Accepts voice input from users.
- Sends audio to an external API for transcription and automated annotation.
- Displays the results to a human annotator for review and correction.
- Allows exporting corrected annotations in a structured format (e.g., JSON or CSV).

### Target Users
- Human annotators and linguists.
- AI training teams needing high-quality labeled audio data.
- Organizations involved in speech AI development and model tuning.

---

## 2. Functional Requirements

### 2.1. Audio Ingestion
- Upload audio file (WAV, MP3, FLAC formats).
- Record voice in-browser using a microphone.
- Show waveform preview and playback.

### 2.2. API Integration
- Send audio to an external **Transcription + Annotation API**.
- Handle authentication (e.g., API keys or OAuth).
- Support async callback or polling model for processing.

#### Data Flow:
1. Audio uploaded or recorded.
2. POST to `/transcribe-annotate` endpoint with file.
3. Receive response:
   ```json
   {
     "transcript": "Hello world",
     "annotations": [
       {"word": "Hello", "start_time": 0.0, "end_time": 0.5, "tag": "greeting"},
       {"word": "world", "start_time": 0.5, "end_time": 1.0, "tag": "object"}
     ]
   }
