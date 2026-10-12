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

## Datenschutz

- Impressum und Datenschutzerklärung liegen zentral auf `start.icken.eu` (`impressum.html`, `datenschutz.html`) und sind im Footer der Seite verlinkt.
- Beim Aufruf der Seite werden keine externen Server kontaktiert: jsQR liegt lokal unter `vendor/jsqr/` (Apache-2.0).
- Das Spotify-Web-Playback-SDK (`sdk.scdn.co`) wird erst **nach dem Login** per `loadSpotifySdk()` nachgeladen. Vor dem Klick auf „Mit Spotify verbinden“ steht ein Datenschutzhinweis auf der Login-Seite.
- Tokens liegen nur im `sessionStorage`, nichts davon geht an unseren Server. Die Kamerabilder werden nur lokal ausgewertet.
- Wer Scopes ändert, muss den Abschnitt „Hitster“ in der Datenschutzerklärung anpassen (aktuell: `streaming user-read-email user-read-private user-modify-playback-state`).
- Der Footer enthält „Abmelden“ (löscht die Tokens im `sessionStorage`) und einen Link zum Widerruf des App-Zugriffs unter <https://www.spotify.com/account/apps/>. Die Spotify Developer Policy verlangt einen leicht erreichbaren Weg, die Verbindung zu trennen, und eine Datenschutzerklärung (die zentrale auf `start.icken.eu`).
