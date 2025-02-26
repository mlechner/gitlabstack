GitLab und GitLab Runner Setup mit Docker Compose

Dieses Repository enthält eine Konfiguration, um GitLab und mehrere GitLab Runner mithilfe von Docker Compose zu betreiben. LDAP wird für die Authentifizierung verwendet, und diese Konfiguration ermöglicht anonymen LDAP-Bind.

Voraussetzungen

- Docker und Docker Compose installiert auf deiner Maschine
- Zugriff auf einen LDAP-Server
- Ein gültiges Registrierungstoken für GitLab Runner

Dateien

- `docker-compose.yml`: Diese Datei beschreibt die Docker-Dienste und Netzwerke.
- `.env`: Diese Datei beinhaltet Umgebungsvariablen für die Konfiguration von GitLab und den GitLab Runner.

Konfiguration

.env Datei

Trage die notwendigen Informationen in die `.env` Datei ein:

``
Host und Ports
GITLAB_HOST=dev-lem-fr.lab.bfs.de
GITLABHTTPPORT=8080
GITLABHTTPSPORT=8443
GITLABSSHPORT=2222

LDAP Konfiguration
LDAP_SERVER=slave-foo.bar.de
LDAP_PORT=7389
LDAP_BASE=dc=bfs,dc=de
LDAP_UID=uid
LDAPBINDDN=""  Leer lassen für anonymen Bind

GitLab Runner Registrierung
REGISTRATION_TOKEN=yourregistrationtokenhere
``

docker-compose.yml Datei

Die `docker-compose.yml` Datei ist so konfiguriert, dass sie die Werte aus der `.env` Datei verwendet. Stelle sicher, dass die Datei für deine Umgebung geeignet ist.

Verwendung

1. Stelle sicher, dass Docker und Docker Compose installiert sind.
2. Bearbeite die `.env` Datei und gebe die erforderlichen Details ein.
3. Starte die Container mit dem folgenden Befehl:

   ```bash
   docker-compose up -d
   ```

4. Greife auf GitLab über `http://${GITLABHOST}:${GITLABHTTP_PORT}` zu und überprüfe die Log-Dateien in den entsprechenden Volumes bei Bedarf.

Skalierung der GitLab Runner

Um die Anzahl der GitLab Runner anzupassen, bearbeite den `replicas` Wert in der `docker-compose.yml` Datei oder verwende Docker Compose-Befehle, um die Anzahl der Replikate dynamisch zu steuern.

bash
docker-compose up --scale gitlab-runner=<ANZAHL>


Hinweise

- Vergewissere dich, dass dein LDAP-Server anonyme Binds zulässt, wenn kein Bind-DN und Passwort verwendet werden.
- Diese Konfiguration verwendet Basis-Ports. Stelle sicher, dass die Ports auf deinem Docker-Host nicht bereits belegt sind.
- Weitere Hinweise findest Du im Unterordner ./docs/

Support

Wenn du Fragen oder Probleme hast, kontaktiere bitte deinen Administrator oder die entsprechende IT-Abteilung.
