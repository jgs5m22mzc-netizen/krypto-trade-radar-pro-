KRYPTO TRADE RADAR – CLOUDFlARE WORKER
=====================================

WICHTIG: Die ZIP-Datei ist ein vollständiges Wrangler-Projekt, kein reiner HTML-Upload. Ein bestehender Cloudflare Worker kann damit per Wrangler aktualisiert werden. Keine API-Schlüssel in Dateien eintragen!

Funktionen: Binance USDⓈ-M Futures Testnet standardmäßig, BTC/ETH/SOL, 5m/15m/1h/4h, RSI/MACD/EMA, manuelle MARKET-Orders, Kontostand/Positionen. Kein Autotrading, keine automatische Stop-Loss/Take-Profit-Absicherung, keine Hebel-Einstellung.

VORAUSSETZUNGEN: Cloudflare-Account, Node.js und npm auf einem PC/Mac oder eine Entwicklungsumgebung mit Terminal. Auf dem iPhone allein lässt sich dieses Projekt nicht über die einfache HTML-Upload-Oberfläche veröffentlichen.

1. ZIP entpacken, Terminal im Ordner trade-radar öffnen.
2. npx wrangler login
3. npx wrangler secret put ADMIN_PASSWORD
   Starkes, einzigartiges Radar-Passwort eingeben.
4. npx wrangler secret put SESSION_SECRET
   Mindestens 32 zufällige Zeichen eingeben (anders als Passwort).
5. Binance Futures TESTNET API-Key und Secret anlegen, mit Futures-Handelsberechtigung; Auszahlungen deaktiviert lassen.
6. npx wrangler secret put BINANCE_API_KEY
7. npx wrangler secret put BINANCE_API_SECRET
8. npx wrangler deploy
9. Die ausgegebene workers.dev-Adresse auf dem iPhone in Safari öffnen. Anmelden, Analyse testen und mit winzigen Testnet-Orders prüfen.
10. Safari > Teilen > Zum Home-Bildschirm.

HINWEIS ZU VORHANDENER WORKER-ADRESSE: wrangler.toml verwendet den Namen krypto-trade-radar. Wenn du deinen vorhandenen Worker ersetzen willst, ändere den Namen auf dessen exakten Worker-Namen und sichere dessen bisherige Dateien vorher. Deploy überschreibt den gewählten Worker.

ECHTGELD: Standardmäßig ausgeschlossen. Nur nach eigener bewusster Entscheidung TRADING_MODE=live setzen und zusätzlich ENABLE_LIVE_TRADING als Servervariable exakt YES_I_ACCEPT_THE_RISK setzen, neue LIVE-Binance-Schlüssel sicher hinterlegen und neu deployen. Beachte Binance-Regionalverfügbarkeit, Konto-Freigaben, API-IP-Whitelist und die rechtlichen Einschränkungen für Futures in deinem Land. Cloudflare-Worker haben ggf. keine feste Ausgangs-IP. Wenn Binance eine feste API-IP-Whitelist verlangt, ist zusätzliche Architektur nötig. Verwende vor Echtgeldhandel Cloudflare Access als zweite Zugangsschicht und konfiguriere Rate Limiting. Diese Beispielimplementierung ist nicht als gehärtete produktive Trading-Plattform auditiert.

SICHERHEIT: Das Passwort wird serverseitig geprüft, die Sitzung ist 8 Stunden gültig, signiert und als HttpOnly/Secure/SameSite-Cookie gesetzt. API-Secrets werden als Cloudflare Worker Secrets gespeichert, nicht im Browser. Die Anwendung hat keine persistente Order-Historie und keinen Schutz gegen doppelte Ausführung bei unklaren Netzwerkausfällen. Ordermenge ist Basiswährung, nicht USDT. Die API erwartet One-way Mode; bei Hedge Mode muss die Orderlogik angepasst werden.

ANALYSE: EMA 20/50, MACD 12/26/9 und RSI 14 als einfache Heuristik, keine validierte Prognose. Die Analyse setzt keine Orders. Für echtes Risikomanagement sind separate Stop-Orders, Tick-/Lot-Size-Prüfung, Positionslimits, Idempotenz und vollständiges Audit-Logging erforderlich.

DOKUMENTATION:
https://developers.cloudflare.com/workers/configuration/secrets/
https://developers.cloudflare.com/workers/static-assets/binding/
https://developers.binance.com/docs/derivatives/usds-margined-futures/trade/rest-api/New-Order
