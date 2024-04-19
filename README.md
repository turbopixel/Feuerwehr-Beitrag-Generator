# Feuerwehr-Beitrag-Generator

Erstelle ein Social Media Post für Facebook und Instagram für deine Feuerwehr in Sekunden. Dieser Fork ist angepasst für die Freiwillige Feuerwehr Werdau.

Website: [112.ovtec.it](https://112.ovtec.it/)

## vite Konfiguration

[Vite Configuration Reference](https://vitejs.dev/config/).

## Mitmachen

Dieses Projekt ist in vue.js mit vite entwickelt. Führe auf deiner Konsole die folgenden
Befehle aus, um an diesem Projekt mitzumachen.

### Lokal ausführen

#### npm Pakete installieren

```sh
npm install
```

#### Projekt lokal ausführen mit hot-reload

```sh
npm run dev
```

#### Projekt kompilieren

```sh
npm run build
```

### Mit Docker entwickeln/veröffentlichen

#### Docker image erzeugen

```sh
docker build -t <your-dockerid>/ffpostcreator .
docker run -it -p 8080:80 --rm --name ffpostcreator <your-dockerid>/ffpostcreator:latest
```

Die App ist jetzt zum lokalen Testen unter [http://127.0.0.1:8080/](http://127.0.0.1:8080/) erreichbar

#### Docker Image veröffentlichen

```sh
docker login -u <your-username> --password-stdin
# Passwort nach Aufforderung eingeben
# Ein erfolgreicher Login wird mit 'Login Succeeded' angezeigt

docker push <your-dockerid>/ffpostcreator
# ohne Angabe eines Tags (: nach dem Namen) wird der Tag 'latest' verwendet
```

#### Deployment

Für die Veröffentlichung der App empfiehlt es sich einen Reverseproxy mit HTTPS wie nginx davor zu setzen.

Beispiel via Docker Compose:

```sh
  ffpostcreator:
    image: <your-dockerid>/ffpostcreator:latest
    container_name: ffpostcreator
    labels:
      - com.centurylinklabs.watchtower.enable=true # when using watchtower for automatic updates
    ports:
      - 8095:80
    restart: unless-stopped
```
