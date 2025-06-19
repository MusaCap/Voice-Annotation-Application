# Voice Annotation Application - Data Model

---

## 📦 Core Entities

### 1. User
Represents a human annotator or admin.

| Field        | Type      | Description                         |
|--------------|-----------|-------------------------------------|
| id           | UUID      | Unique user ID                      |
| name         | String    | Full name                           |
| email        | String    | Login email                         |
| role         | Enum      | ['annotator', 'admin', 'viewer']    |
| created_at   | Timestamp | Account creation time               |
| last_login   | Timestamp | Last active session                 |

---

### 2. AudioFile
Stores uploaded or recorded voice input.

| Field        | Type      | Description                          |
|--------------|-----------|--------------------------------------|
| id           | UUID      | Unique audio ID                      |
| filename     | String    | Original file name                   |
| filepath     | String    | URL or storage reference             |
| duration     | Float     | In seconds                           |
| uploaded_by  | UUID      | `User.id`                            |
| project_id   | UUID      | Optional reference to a `Project`    |
| created_at   | Timestamp | Upload timestamp                     |

---

### 3. Transcription
Auto-generated transcript tied to an audio file.

| Field        | Type      | Description                          |
|--------------|-----------|--------------------------------------|
| id           | UUID      | Unique ID                            |
| audio_id     | UUID      | `AudioFile.id`                       |
| text         | Text      | Full transcript                      |
| status       | Enum      | ['pending', 'completed', 'failed']   |
| source_api   | String    | Name of API used (e.g., Whisper)     |
| created_at   | Timestamp | Timestamp when generated             |

---

### 4. Annotation
Represents one unit of annotation (typically per word or phrase).

| Field            | Type      | Description                        |
|------------------|-----------|------------------------------------|
| id               | UUID      | Unique annotation ID               |
| transcription_id | UUID      | `Transcription.id`                 |
| word             | String    | Annotated word or phrase           |
| start_time       | Float     | Start time in seconds              |
| end_time         | Float     | End time in seconds                |
| tag_id           | UUID      | Optional `Tag.id`                  |
| created_by       | UUID      | `User.id` of annotator             |

---

### 5. Correction
Tracks manual changes to transcript or annotations.

| Field          | Type      | Description                          |
|----------------|-----------|--------------------------------------|
| id             | UUID      | Unique ID                            |
| annotation_id  | UUID      | `Annotation.id`                      |
| old_word       | String    | Original word or tag                 |
| new_word       | String    | Corrected version                    |
| user_id        | UUID      | `User.id` who made the change        |
| timestamp      | Timestamp | Time of correction                   |
| note           | Text      | Optional explanation or context      |

---

### 6. Tag
Reusable classification labels for annotations.

| Field        | Type      | Description                          |
|--------------|-----------|--------------------------------------|
| id           | UUID      | Unique tag ID                        |
| label        | String    | e.g., "greeting", "object"           |
| color_code   | String    | HEX or CSS color code                |
| description  | String    | Tag description                      |

---

### 7. Comment
User notes tied to annotations or audio.

| Field          | Type      | Description                          |
|----------------|-----------|--------------------------------------|
| id             | UUID      | Unique comment ID                    |
| user_id        | UUID      | Who left the comment                 |
| annotation_id  | UUID      | (Optional) Related annotation        |
| audio_id       | UUID      | (Optional) Whole audio comment       |
| text           | Text      | Comment content                      |
| timestamp      | Timestamp | When the comment was created         |

---

### 8. Export
Tracks output generation for downstream use.

| Field        | Type      | Description                          |
|--------------|-----------|--------------------------------------|
| id           | UUID      | Export ID                            |
| audio_id     | UUID      | Which audio was exported             |
| user_id      | UUID      | Who exported                         |
| format       | Enum      | ['JSON', 'CSV']                      |
| content      | Text/Blob | File content or reference link       |
| exported_at  | Timestamp | Time of export                       |

---

### 9. Project *(optional)*
For grouping audio files, users, and annotations.

| Field        | Type      | Description                          |
|--------------|-----------|--------------------------------------|
| id           | UUID      | Project ID                           |
| name         | String    | Descriptive name                     |
| description  | Text      | Project overview                     |
| owner_id     | UUID      | User who created it                  |
| created_at   | Timestamp | Creation time                        |

---

## 🔗 Entity Relationships (ERD Summary)

- `User` has many `AudioFile`, `Correction`, `Comment`, `Export`
- `AudioFile` has one `Transcription`, belongs to `Project`
- `Transcription` has many `Annotation`
- `Annotation` has one optional `Tag`, and many `Correction` and `Comment`
- `Export` refers to one `AudioFile`
- `Project` groups multiple `AudioFile`

---

## ☁️ Storage Notes

- **Audio files:** Cloud storage (e.g., AWS S3 or Firebase)
- **Database:** Relational (PostgreSQL) or hybrid schema (e.g., MongoDB)
- **Versioning:** Store all `Correction` records for auditability

---

## 🛠 Future Considerations

- Support version history per `Annotation` and `Transcription`
- Add review workflows (e.g., second-level QA)
- Include confidence scores in `Annotation`

