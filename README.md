# CricFAN Android-ready web app

This folder contains:
- `index.html`
- `styles.css`
- `index.js`

## Important: real live scores
No ESPN live API key is included. ESPN does not provide a universal public API key that can be safely handed out for arbitrary use. Do not scrape ESPN endpoints or expose a private provider key in a public client app.

To connect real scores:
1. Choose a cricket data provider and obtain your own API access/key, or use an authorized backend service.
2. Configure `CRICFAN_API_URL` in `index.js` to point to your backend endpoint.
3. If you use a private key, keep it on your backend. Do not put it in `index.js` in a publicly distributed app.
4. Return JSON normalized to this shape:

```json
{
  "matches": [
    {
      "id": "unique-match-id",
      "category": "INTERNATIONAL",
      "status": "live",
      "series": "Series name",
      "format": "T20I",
      "venue": "Venue",
      "note": "Current match status",
      "teams": [
        {"name": "Team A", "score": 123, "wickets": 4, "overs": "14.2", "summary": "Batting"},
        {"name": "Team B", "score": 0, "wickets": 0, "overs": "0.0", "summary": "Yet to bat"}
      ],
      "result": "",
      "updatedAt": "2026-10-18T00:00:00Z"
    }
  ]
}
```

The interface polls every second only when configured, but score freshness depends on the provider and its rate limits. Many APIs do not allow 1-second requests. Follow your plan's terms and rate limits.

## Run it
Open `index.html` in a browser or serve the folder from a local web server. To package as an Android APK, wrap this web app with Android Studio WebView, Capacitor, or another Android packaging workflow. This folder alone is a responsive web app, not a signed APK.

## Manual scoring
Create a match in the Scoring Desk, select it from the match list, then use the ball buttons. Manual matches are in-memory only and are not persisted after refresh. For production use, add a backend/database and test cricket scoring rules carefully (e.g. run-outs, penalty runs, strike changes, extras and Test innings).
