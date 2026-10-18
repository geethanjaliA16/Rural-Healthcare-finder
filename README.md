🌾 GramCare — Rural Healthcare Access Finder
Because care shouldn't depend on distance.

GramCare is a web platform that helps rural residents answer three questions when someone falls sick: where to go, how urgent it is, and whether they can afford treatment. It guides users through one connected journey, from symptom check to nearby facility to government health scheme eligibility, with one-tap access to the 108 ambulance service on every page.

Built for Smart India Hackathon 2026 under the theme Agriculture, FoodTech & Rural Development.

🎯 Problem
Healthcare access in rural Karnataka is uneven. Karnataka's Health Department audit (April 2025) found that over 70% of the state's 464 maternal deaths in 2024 were preventable, with districts such as Kalaburagi, Dharwad and Belagavi among the most affected. Rural families often face three unknowns at once:

Which nearby facility is reachable and has a doctor available?
Is the condition urgent enough to travel?
Can we afford treatment, or do we qualify for a government scheme?
This uncertainty delays care. GramCare aims to remove it.

✨ Features
Step	Feature	Details
1	Login	Name + phone number, no password (stored in the browser)
2	Symptom Check	Select from a checklist, type your own, or speak symptoms (voice input); rule-based urgency result: urgent / moderate / minor
3	Find Facility	Auto-filtered by recommended facility type; search by village/taluk name or GPS; shows doctor availability, distance and phone; view on map and share location via Google Maps link
4	ASHA Worker Connect	Shows the local ASHA (Accredited Social Health Activist) worker's contact for the searched area
5	Health Schemes	Checks eligibility for schemes such as Ayushman Bharat based on income and state
★	Emergency Access	One-tap 108 call button on every page, available even before login

🧱 Tech Stack
Frontend: HTML, CSS, JavaScript, Leaflet.js, Web Speech API
Backend: Python, Flask, Flask-CORS
Data: CSV files (facilities, ASHA workers, schemes)
Services: OpenStreetMap Nominatim (geocoding), browser Geolocation API
Logic: transparent rule-based triage (no black-box ML), Haversine distance calculation, fuzzy substring matching for free-text input

📁 Project Structure
rural-healthcare-finder/
├── backend/
│   ├── app.py                  # Flask entry point
│   ├── requirements.txt
│   ├── routes/
│   │   ├── facilities.py       # nearby + name search
│   │   ├── triage.py           # symptom urgency logic
│   │   ├── schemes.py          # scheme eligibility
│   │   └── asha.py             # ASHA worker lookup
│   └── data/
│       ├── facilities.csv
│       ├── asha_workers.csv
│       └── schemes.csv
├── frontend/
│   ├── index.html
│   ├── login.html
│   ├── symptom-check.html
│   ├── facility-finder.html
│   ├── schemes.html
│   ├── css/style.css
│   └── js/                     # api, auth, map, triage, schemes
└── README.md

🚀 Getting Started
Prerequisites
Python 3.8+
A modern browser (Chrome/Edge recommended for voice input)
Run the backend
bash
cd backend
pip install -r requirements.txt
python app.py        # on Windows: py app.py

The API runs at http://127.0.0.1:5000.

Run the frontend

Open frontend/login.html in your browser (or serve the folder with python -m http.server 8000). The backend must be running.

🔌 API Endpoints
Method	Endpoint	Description
GET	/api/facilities?lat=&lng=	Nearest facilities to a coordinate
GET	/api/facilities/search?q=	Search facilities by village/taluk/name
POST	/api/triage	{ "symptoms": [...] } → urgency + recommended facility types
POST	/api/schemes	{ "income", "state" } → eligible schemes
GET	/api/asha-worker?q=	ASHA worker for a village/taluk

⚠️ Current Limitations (Prototype)
Facility data is a demo dataset for Mandya district, Karnataka; ASHA worker contacts and scheme data are representative samples, not live government data.
Doctor availability is static, not synced with real staff schedules.
Symptom triage is guidance only, not a medical diagnosis.
Login is client-side only (no OTP or server-side authentication).
Map tiles and location search need an internet connection.
English-only interface for now.

🗺️ Roadmap
 Integrate real Karnataka Health Department facility and scheme data
 Live doctor-availability updates
 Kannada and Hindi language support
 Offline / SMS fallback for low-connectivity areas
 OTP-based login
 Expand coverage to Kalaburagi, Dharwad and Raichur
 
📚 References
Karnataka Health Department — Maternal Death Audit Report (April 2025)
Ayushman Bharat PM-JAY, ASHA programme (Ministry of Health & Family Welfare)
OpenStreetMap / Nominatim, Leaflet.js, Flask documentation
