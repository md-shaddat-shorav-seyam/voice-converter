# voice-converter


# 🎤 Voice Conversion API (Flask)

A simple Flask-based REST API that allows users to upload an audio file and convert its **pitch** and **speed (tempo)** using `librosa`. The processed audio is returned as a downloadable WAV file.

---

## 🚀 Features

* Upload audio files via HTTP POST
* Pitch shifting (up or down)
* Tempo (speed) adjustment
* Returns processed audio as `.wav`
* CORS enabled (frontend-friendly)
* Automatic cleanup of temporary files

---

## 🧰 Tech Stack

* **Backend:** Flask
* **Audio Processing:** librosa, soundfile
* **Utilities:** uuid, os
* **CORS Support:** flask-cors

---

## 📦 Requirements

Install required dependencies:

```bash
pip install flask flask-cors librosa soundfile
```

> ⚠️ `librosa` may require system dependencies like `ffmpeg` or `libsndfile` on Linux.

---

## ▶️ Running the Server

```bash
python app.py
```

The server will start at:

```
http://localhost:5000
```

---

## 🔌 API Endpoint

### `POST /convert-voice`

Uploads an audio file and applies pitch and speed modifications.

---

### 📥 Request

**Content-Type:** `multipart/form-data`

#### Form Fields

| Field | Type  | Required | Default | Description                 |
| ----- | ----- | -------- | ------- | --------------------------- |
| file  | File  | ✅ Yes    | —       | Audio file (wav, mp3, etc.) |
| pitch | Float | ❌ No     | `4`     | Pitch shift in semitones    |
| rate  | Float | ❌ No     | `1.05`  | Playback speed (tempo)      |

---

### 📤 Response

* **Success:**

  * Returns processed audio file (`audio/wav`)
  * Download starts automatically

* **Error Responses:**

| Status Code | Message                     |
| ----------- | --------------------------- |
| 400         | No file uploaded            |
| 400         | Invalid pitch or rate value |

Example error response:

```json
{
  "error": "No file uploaded"
}
```

---

## 🧠 How It Works

1. Audio file is uploaded and saved temporarily
2. Audio is loaded using `librosa`
3. Pitch is adjusted using `librosa.effects.pitch_shift`
4. Speed is modified using `librosa.effects.time_stretch`
5. Processed audio is saved as a new WAV file
6. File is sent back to the client
7. Temporary input file is deleted automatically

---

## 🔧 Core Function

### `process_audio(audio_path, pitch_steps, rate)`

**Parameters:**

* `audio_path` – Path to input audio file
* `pitch_steps` – Pitch shift in semitones
* `rate` – Speed multiplier

**Returns:**

* Path to processed `.wav` file

---

## 🧪 Example (cURL)

```bash
curl -X POST http://localhost:5000/convert-voice \
  -F "file=@voice.mp3" \
  -F "pitch=3" \
  -F "rate=1.1" \
  --output output.wav
```

---

## 🌐 Frontend Compatibility

* CORS is enabled using `flask-cors`
* Works with:

  * React
  * Vue
  * Vanilla JS
  * Mobile apps

---


