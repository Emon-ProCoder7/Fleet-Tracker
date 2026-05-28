# FleetLive: Real-Time GPS Cockpit

FleetLive is a high-fidelity vehicle tracking simulation built for the Rio Deep Technologies assessment. It visualizes multiple vehicle types navigating the real-world road network of Dhaka City in real time.

## 🚀 Live Production URL
**[https://fleetlive.vercel.app/](https://fleetlive.vercel.app/)**

## 🛠 Tech Stack
- **Frontend:** Vanilla JS, Tailwind CSS, Leaflet.js (Map SDK).
- **Backend Orchestration:** n8n.
- **Database:** Supabase (PostgreSQL).
- **Routing Engine:** OpenRouteService API (Real road geometry).
- **Design Aesthetic:** Obsidian/Geist (Modern High-Contrast UI).

## 🧠 System Architecture & Logic
The system simulates real GPS movement via an automated coordinate-advancement engine:
1. **Vehicle Registration:** When a user registers a vehicle, a POST request triggers a webhook.
2. **Dynamic Pathfinding:** The backend generates random start/end coordinates within Dhaka and fetches a real road-network path using **OpenRouteService**.
3. **State Management:** Metadata and full path arrays are stored in **Supabase**.
4. **Heartbeat Simulation:** Every 5 seconds, an n8n background schedule advances the `current_index` for all active vehicles.
5. **Arrival Logic:** To maintain a realistic simulation, vehicles track their progress along the road path and come to a stop once they reach their final destination point.
6. **Frontend Polling:** The cockpit polls the state every 3 seconds, using CSS transitions to ensure smooth, "gliding" icon movement across the map.

## ⚙️ Installation & Replicability
1. Clone the repository.
2. Open `index.html` in a browser (or host via Vercel/GitHub Pages).
3. **Backend Setup:**
   - Import `workflow.json` into n8n.
   - Configure a Supabase table named `vehicles` with: `id (PK)`, `name`, `type`, `latitude`, `longitude`, `current_index (int4)`, `route_geometry (text)`.
   - Update Webhook URLs in the `<script>` section of `index.html`.

## 📝 Assessment Deliverables Checklist
- [x] **Vehicle Registration:** Simple UI for Car, Motorcycle, and Rickshaw.
- [x] **Live Location Tracking:** Markers move smoothly on a live map.
- [x] **Use of Free Tools:** OpenStreetMap, Leaflet, n8n, Supabase.
- [x] **Realistic Movement:** Vehicles follow actual roads and stop at destinations.
