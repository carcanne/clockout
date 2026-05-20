# ClockOut 2.0

A full-stack web application that helps employees determine their clock-out time based on captured work hours. The app uses OCR (Optical Character Recognition) to extract times from images and automatically calculates the end time based on lunch breaks and target working hours.

## Features

- **OCR Image Processing**: Extract clock times from images of timecards or schedules
- **Automatic Calculation**: Calculate end-of-work time based on:
  - Start/pause times captured from images
  - Lunch break duration
  - Target working hours
- **Menu Management**: Retrieve and display available menus
- **Cross-Origin Support**: CORS-enabled API for seamless frontend-backend communication
- **Responsive UI**: Vue 3 frontend with TypeScript support

## Tech Stack

### Backend
- **Framework**: FastAPI (Python)
- **OCR**: EasyOCR
- **Dependencies**: Pydantic, Beautiful Soup, Pillow, isodate

### Frontend
- **Framework**: Vue 3
- **Language**: TypeScript
- **Build Tool**: Vite
- **Node Version**: ^20.19.0 || >=22.12.0

## Project Structure

```
clockout/
├── python_backend/              # Backend application
│   ├── main.py                 # FastAPI application & endpoints
│   ├── func.py                 # Time calculation logic
│   ├── get_menus.py            # Menu retrieval
│   ├── ocr.py                  # OCR image processing
│   └── requirements.txt         # Python dependencies
├── vue-frontend-clockout/       # Frontend application
│   ├── src/
│   │   ├── App.vue             # Main app component
│   │   ├── main.ts             # Entry point
│   │   └── views/
│   │       └── clockoutView.vue # Clock-out view
│   ├── package.json            # Node dependencies
│   └── vite.config.ts          # Vite configuration
├── request.http                # API request examples
└── README.md                   # This file
```

## Setup & Installation

### Prerequisites
- Python 3.8+
- Node.js ^20.19.0 || >=22.12.0
- npm

### Backend Setup

1. Navigate to the backend directory:
   ```bash
   cd python_backend
   ```

2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

### Frontend Setup

1. Navigate to the frontend directory:
   ```bash
   cd vue-frontend-clockout
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

## Running the Application

### Start Backend
```bash
cd python_backend
python main.py
```
The API will be available at `http://localhost:8000`

### Start Frontend
```bash
cd vue-frontend-clockout
npm run dev
```
The frontend will be available at `http://localhost:5371`

## API Endpoints

### Process Image & Calculate End Time
**POST** `/process-img`

Send a base64-encoded image containing clock times.

**Request Body:**
```json
{
  "data": "<base64-encoded-image>"
}
```

**Response:**
```json
{
  "end_time": "2026-01-22T17:45:00+01:00",
  "times": ["2026-01-22T12:14:00+01:00", "2026-01-22T11:31:00+01:00", "2026-01-22T07:41:00+01:00"]
}
```

### Get Menus
**GET** `/menus`

Retrieve available menu information.

**Response:**
```json
{
  "1": {"name": "Menu Name", "desc": "Menu Description"},
  "2": {"name": "Another Menu", "desc": "Description"}
}
```

## Build for Production

### Frontend
```bash
cd vue-frontend-clockout
npm run build
npm run type-check  # Type checking with TypeScript
```

## CORS Configuration

The backend allows requests from:
- `https://www.clockout.ch`
- `https://clockout.ch`
- `http://localhost:5371` (local development)

Modify the `origins` list in `python_backend/main.py` to allow additional domains.

## Development

### Type Checking (Frontend)
```bash
cd vue-frontend-clockout
npm run type-check
```

### Preview Production Build
```bash
npm run preview
```

## License

This project underlies the Apachee licence 2.0

---

For more information, visit [clockout.ch](https://www.clockout.ch)