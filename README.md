# Hitster Web-Player

Statische Website (eine `index.html`, kein Backend) zum Scannen der
selbstgebauten Hitster-QR-Codes: der erkannte Song wird über Spotify
abgespielt, ohne Titel/Interpret zu zeigen.

**Live:** https://hitster.icken.eu

## Voraussetzungen

- Spotify Premium (für jede Person, die sich einloggt)
- Browser mit Kamera-Zugriff
- Spotify-App im Developer Dashboard im **Development Mode**, bis zu 25
  Tester-Accounts unter User Management freischalten

## Konfiguration

`CLIENT_ID` steht oben im `<script>`-Block in `index.html` (kein Secret
nötig, Login läuft per PKCE). Im Spotify-Dashboard muss unter
**Redirect URIs** exakt `https://hitster.icken.eu/` eingetragen sein.
HTTPS ist Pflicht (Kamera + `crypto.subtle`).

## Deployment

Repo per Git auf dem Netcup-Webhosting klonen (Plesk-Git-Erweiterung
oder `git clone` per SSH), Document Root der Domain auf den Ordner mit
`index.html` setzen. Updates: pushen, auf dem Server `git pull`.

## Troubleshooting

- `redirect_uri: Not matching configuration` → Redirect-URI im Dashboard
  prüfen (Kopieren-Button auf der Login-Seite nutzen).
- Login-Button tut nichts → fehlendes HTTPS.
- Login ok, keine Wiedergabe → kein Premium-Account.
- Seite hängt bei "Verbinde mit Spotify…" → Ad-/Trackingblocker blockiert
  `sdk.scdn.co`.
