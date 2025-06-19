# 📋 Voice Annotation Application – Product Backlog

---

## 🧩 Epic 1: Audio Upload & Recording

### ✅ User Story 1.1: As a user, I want to upload audio files so that they can be transcribed.
- [ ] Task 1.1.1: Implement file picker (WAV, MP3, FLAC support)
- [ ] Task 1.1.2: Validate audio duration and file type
- [ ] Task 1.1.3: Store audio in backend/cloud storage
- [ ] Task 1.1.4: Display file name and upload status

### ✅ User Story 1.2: As a user, I want to record audio directly from my browser.
- [ ] Task 1.2.1: Use Web Audio API to capture microphone input
- [ ] Task 1.2.2: Visualize waveform in real-time
- [ ] Task 1.2.3: Save and upload recorded file to backend

**Priority**: High  
**Dependencies**: None

---

## 🔄 Epic 2: Transcription & API Integration

### ✅ User Story 2.1: As a user, I want the app to automatically send my audio to a transcription service.
- [ ] Task 2.1.1: Integrate with transcription API (e.g., Whisper)
- [ ] Task 2.1.2: Handle API authentication
- [ ] Task 2.1.3: Poll or subscribe to job completion
- [ ] Task 2.1.4: Store transcript and annotations in DB

### ✅ User Story 2.2: As a user, I want to see a loading state while transcription is in progress.
- [ ] Task 2.2.1: Add spinner/loading animation
- [ ] Task 2.2.2: Show progress or ETA if available

**Priority**: High  
**Dependencies**: Epic 1 completion

---

## 📝 Epic 3: Annotation Interface

### ✅ User Story 3.1: As an annotator, I want to see transcribed text broken down word-by-word with timestamps.
- [ ] Task 3.1.1: Create timeline-linked word segments
- [ ] Task 3.1.2: Highlight word as audio plays

### ✅ User Story 3.2: As an annotator, I want to assign tags to words or phrases.
- [ ] Task 3.2.1: Create tag dropdown menu
- [ ] Task 3.2.2: Support color-coded tag highlighting
- [ ] Task 3.2.3: Allow manual tag entry (optional)

### ✅ User Story 3.3: As an annotator, I want to correct transcription errors directly.
- [ ] Task 3.3.1: Enable inline editing of words
- [ ] Task 3.3.2: Store edits and track versions

**Priority**: High  
**Dependencies**: Epic 2 completion

---

## 🛠️ Epic 4: Annotation Tools & QA Features

### ✅ User Story 4.1: As an annotator, I want undo/redo functionality.
- [ ] Task 4.1.1: Track change history stack
- [ ] Task 4.1.2: Implement undo/redo keyboard shortcuts

### ✅ User Story 4.2: As an annotator, I want to leave comments tied to specific audio segments.
- [ ] Task 4.2.1: Enable comment input on word or phrase
- [ ] Task 4.2.2: Display comment markers in UI

### ✅ User Story 4.3: As a reviewer, I want to view a history of all changes made.
- [ ] Task 4.3.1: Log user corrections in DB
- [ ] Task 4.3.2: Create revision view or side panel

**Priority**: Medium  
**Dependencies**: Epic 3

---

## 📤 Epic 5: Export & Delivery

### ✅ User Story 5.1: As a user, I want to export the corrected transcript and annotations in JSON or CSV format.
- [ ] Task 5.1.1: Build export formatter for JSON
- [ ] Task 5.1.2: Build CSV export option
- [ ] Task 5.1.3: Add "Download Export" button

**Priority**: Medium  
**Dependencies**: Epic 3

---

## 👥 Epic 6: User Management & Roles

### ✅ User Story 6.1: As an admin, I want to assign roles and permissions to users.
- [ ] Task 6.1.1: Integrate Auth (Firebase/Auth0)
- [ ] Task 6.1.2: Define roles: Admin, Annotator, Viewer
- [ ] Task 6.1.3: Enforce RBAC in frontend/backend

**Priority**: Low (initially)  
**Dependencies**: None

---

## 📈 Epic 7: Project & Session Management

### ✅ User Story 7.1: As a user, I want to group files into projects for easier management.
- [ ] Task 7.1.1: Create project creation UI
- [ ] Task 7.1.2: Link audio to project ID
- [ ] Task 7.1.3: Enable project-level exports

**Priority**: Low  
**Dependencies**: Optional feature layer

---

## ♿ Epic 8: Accessibility & UI Polish

### ✅ User Story 8.1: As a user with a disability, I want the UI to be accessible via keyboard and screen reader.
- [ ] Task 8.1.1: Ensure full keyboard navigation
- [ ] Task 8.1.2: Add ARIA labels and roles
- [ ] Task 8.1.3: Validate contrast & responsive layout

**Priority**: Medium  
**Dependencies**: UI completion from Epic 3 & 4

---

## 🚨 Epic 9: Error Handling & Logging

### ✅ User Story 9.1: As a user, I want clear feedback when an error occurs during upload or transcription.
- [ ] Task 9.1.1: Show toast or modal on failure
- [ ] Task 9.1.2: Store error logs in backend

**Priority**: High  
**Dependencies**: Applies to all major epics

---
