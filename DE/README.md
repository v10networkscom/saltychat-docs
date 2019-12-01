# Salty Chat
Salty Chat ist ein TeamSpeak Plugin, welches für mehr Realismus in Sachen Sprachkommunikation für Spielemods (wie z.B. FiveM, RAGEMP, alt:V, RedM, etc.) sorgt.
Um eine große Breite an Mods zu bedienen, stellt das Plugin einen WebSocket Server bereit, worüber eine bidirektionale Kommunikation erfolgen kann.
Durch die Möglichkeit der Kommunikation in beide Richtungen, kann das Plugin auch "State Trigger" (Spieler redet, Mikrofon ge-/entmuted, Sound ge-/entmuted, etc.) schicken.

Wir stellen für einige Mods verschiedene Ressourcen zur Verfügung und warten diese auch bei Updates oder Problemen.
Da es uns unmöglich ist für jeden Mod und jedes Framework eine Ressource zu stellen, sind wir auf eure Hilfe angewiesen.
Wenn Ihr Ressource für bestimmte Mods oder Frameworks schreibt, welche wir nicht abgedeckt haben, könnt Ihr diese gerne zur Verfügung stellen und wir werden diese verlinken.

Außerdem könnt Ihr gerne unserem [Discord](https://discord.gg/MBCnqSf) beitreten und aktiv an Salty Chat mitarbeiten!

# Features
## Sprache
* 3D Audio
* Einstellbare Reichweiten (für z.B. flüstern und schreien)
* Distanzbasierte Abflachung der Lautstärke

## Funk
* Realistische Stimmenverzerrung
* Verzerrung basierend auf der Distanz
* Verschiedene Reichweiten
  * Ultra Short Range (1,8km)
  * Short Range (3km)
  * Long Range (8km)
* Direkte Kommunikation von Funkgerät zu Funkgerät, oder verteilt über Funktürme (Distributed)
* Lautsprecher (Spieler können den gesamten Funkverkehr mithören)
* Anpassbare 3D Position für die Wiedergabe

## Telefon
* Realistische Stimmenverzerrung
* Verzerrung basierend auf der Signalstärke
* Lautsprecher (Spieler können die Gesprächspartner hören)
* Anpassbare 3D Position für die Wiedergabe

## Audio Player
* Sounds im jeweiligen Sound Pack (`%appdata%\TS3Client\plugins\SaltyChat`) können abgespielt und gestoppt werden
* Mehrere Sounds gleichzeitig abspielen (z.B. ein Klingelton und Vibration)
* Sauberes loopen von Sounds
* Globales Überschreiben von Sounds (`%appdata%\TS3Client\plugins\SaltyChat\override`)

# Konfigurationsdatei
Beim Start des Plugins wird die Konfigurationsdatei unter `%appdata%\TS3Client\plugins\SaltyChat\settings.json` geladen und angewendet.
Hier sind verschiedene Optionen die Angepasst werden können.

Parameter | Wirkung
------------ | -------------
WebSocketAddress | Die Adresse und Port auf welcher der WebSocket Server sich bindet
UpdateBranch | Der Update Branch der über unsere Versions API nach einer neuen Version abgefragt wird
OriginExceptions | Ausnahmen für die Source einer WebSocket Verbindung - surfst du z.B. auf saltmine.de, kann die Webseite sich über lokal ausgeführtes JavaScript sich versuchen mit dem WebSocket zu verbinden, wobei die Source dann `https://saltmine.de` wäre
Is3dEnabled | Aktiviert/Deaktiviert 3D Audio
IsDebugLoggingEnabled | Aktiviert/Deaktiviert debug logging - sollte nur bei Bedarf eingeschaltet werden
PhoneOffset | 3D Position für die Wiedergabe des Telefons
RadioOffset | 3D Position für die Wiedergabe des Funkgerätes
