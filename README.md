# Nixo Express (Fabric, Minecraft 1.21.11)

Server-Mod: Spieler bestellen Kits/Blöcke und schreiben dazu, was sie dafür geben.
Admins sehen alle Bestellungen, sagen Deals zu und bearbeiten das Sortiment.
Läuft nur auf dem Server – Spieler brauchen keine Mod (Vanilla-Client reicht).

## JAR bauen
1. JDK 21 installieren.
2. Auf https://fabricmc.net/develop/ Version 1.21.11 wählen und die Versionen in `gradle.properties`
   (yarn_mappings, loader_version, loom_version, fabric_version) mit den dort angezeigten abgleichen.
3. Gradle-Wrapper erzeugen (einmalig, falls Gradle installiert ist): `gradle wrapper`
   – oder das Template von der Fabric-Seite laden und den Ordner `src/` hierher kopieren.
4. `./gradlew build` (Windows: `gradlew.bat build`)
5. Die Datei `build/libs/nixo-express-1.0.0.jar` (nicht `-sources`) in den `mods/`-Ordner des Servers legen.
   Zusätzlich wird die **Fabric API** auf dem Server benötigt.

## Befehle für Spieler
- `/express` oder `/express list` – Sortiment ansehen (klickbar)
- `/express info <produkt>` – Details
- `/express order <produkt> <was du dafür gibst>` – Bestellung mit Angebot
- `/express orders` – eigene Bestellungen
- `/express cancel <id>` – offene Bestellung stornieren

## Befehle für Admins (OP)
- `/expressadmin orders` – offene Bestellungen (mit Buttons Annehmen/Ablehnen); `orders all` zeigt alle
- `/expressadmin accept <id>` – Deal zusagen: Spieler bekommt Benachrichtigung + die Items
  (offline: beim nächsten Login)
- `/expressadmin deny <id> [grund]` – ablehnen, Spieler wird benachrichtigt
- `/expressadmin product list`
- `/expressadmin product add <id> <name>`
- `/expressadmin product name|desc|price <id> <text>`
- `/expressadmin product additem <id>` – Item in der Hand (inkl. Anzahl) hinzufügen
- `/expressadmin product clearitems <id>`
- `/expressadmin product toggle <id>` – ein-/ausblenden
- `/expressadmin product remove <id>`

Alle Daten liegen in `config/nixo_express.json` und können auch dort von Hand bearbeitet werden
(Server vorher stoppen).

## Hinweise
- Items werden nur nach Typ und Anzahl gespeichert (keine Verzauberungen/Namen).
- Falls die Zeile mit `ADMIN` in `ExpressCommands.java` nicht kompiliert (Berechtigungs-API
  in 1.21.11 geändert), durch `src -> src.hasPermissionLevel(2)` ersetzen.
