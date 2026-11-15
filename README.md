# Ludhiana CropAI — Member 1 Frontend

A React + Vite frontend prototype for farmer registration, field monitoring, moisture-stress estimates and irrigation-priority guidance.

## Run locally

```bash
npm install
npm run dev
```

Open the local URL printed by Vite (usually http://localhost:5173).

## Included

- Farmer registration and login (browser-local demo account)
- Multiple field registration: field name, crop, area, sample village
- Responsive dashboard with personalized greeting and date
- Interactive satellite imagery map with clickable sample field polygons
- Field snapshot, stress labels, estimated water deficit and irrigation ranking
- Field detail view with indicator explanation and decision-support caveat
- API service layer ready to connect to Member 2's backend

## Demo flow

1. Open the app and select **Create account**.
2. Enter a farmer name, a 10-digit Indian mobile number and password.
3. Keep the sample village selected and add one or more fields.
4. Submit to open the dashboard.
5. Click a field polygon or a row in Irrigation Priority to inspect it.
6. Log out and use the same phone/password to log in again on that browser.

## Important prototype notes

- Farmer account details are stored in `localStorage` for the hackathon demo only. This is not production authentication.
- The map uses an Esri World Imagery tile layer and illustrative field polygons around the Ludhiana pilot area. Confirm the chosen pilot boundary and replace the polygons with Member 2's GeoJSON.
- The default field analytics are sample data in `src/data/demoFields.js`. Do not present them as real satellite measurements.
- The crop-health chart is illustrative sample data.
- The frontend service tries the backend first and falls back to sample data if the API is unavailable.

## Backend integration

Set `VITE_API_BASE_URL` in a local `.env` file:

```env
VITE_API_BASE_URL=http://localhost:5000
```

Expected endpoints (as in the team API contract):

- `GET /api/dashboard?area=ludhiana-pilot`
- `GET /api/fields?area=ludhiana-pilot`
- `GET /api/fields/:fieldId`

The dashboard expects `fields[]` records with `id`, `name`, `cropType`, `growthStage`, `stressLevel`, `deficitMm`, `priority`, `geometry` (to be mapped to Leaflet coordinates), and `updatedAt`. Align the adapter in `src/services/cropAiApi.js` with Member 2's exact response shape.

## Suggested next steps for Member 1

- Replace demo polygons with the pilot GeoJSON from Member 2.
- Confirm API response property names and map `geometry` to Leaflet polygon coordinates.
- Add loading/error states for real API failures rather than silently using demo fallback in production.
- Add a proper backend-backed authentication flow before any real farmer data is used.
