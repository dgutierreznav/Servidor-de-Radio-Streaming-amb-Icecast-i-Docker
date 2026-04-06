# Servidor-de-Radio-Streaming-amb-Icecast-i-Docker

# Servidor de Streaming Icecast amb Docker

[cite_start]Aquest projecte consisteix en la implementació d'un servidor de ràdio per streaming utilitzant **Icecast2** i **FFmpeg** com a codificador, tot gestionat mitjançant contenidors **Docker**[cite: 1, 78, 96].

## Estructura del Projecte
[cite_start]L'estructura de directoris necessària per al funcionament del projecte és la següent[cite: 8, 11, 13]:

* [cite_start]`radio-dgutierrez/`: Directori principal[cite: 9].
    * [cite_start]`audio/`: Conté els fitxers de música en format MP3 o Opus[cite: 11, 15, 17].
    * [cite_start]`config/`: Conté el fitxer de configuració `icecast.xml`[cite: 11, 19].
    * [cite_start]`logs/`: Magatzem per als registres d'accés i errors[cite: 11, 50].

## 🛠️ Configuració del Sistema

### 1. Servidor Icecast (`icecast.xml`)
[cite_start]El servidor està configurat amb els següents paràmetres clau[cite: 19, 21, 22]:
* [cite_start]**Límits:** Fins a 50 clients simultanis i 3 fonts d'emissió[cite: 27, 28].
* **Autenticació:**
    * [cite_start]**Source Password:** `Font_dgutierrez_2024`[cite: 37].
    * [cite_start]**Admin Password:** `Admin_dgutierrez_2024`[cite: 40].
* [cite_start]**Xarxa:** Escolta en el port 8000 i utilitza el hostname `radio-dgutierrez.local`[cite: 43, 45].

### 2. Desplegament amb Docker Compose
[cite_start]El fitxer `docker-compose.yml` defineix dos serveis principals[cite: 78, 80]:
* [cite_start]**icecast-dgutierrez:** Utilitza l'imatge `moul/icecast` i munta els volums de configuració i logs[cite: 81, 82, 87, 88].
* [cite_start]**streamer-dgutierrez:** Utilitza `linuxserver/ffmpeg` per codificar i enviar l'àudio al servidor[cite: 95, 96].

## 📻 Punts de Muntatge Disponibles
[cite_start]S'han configurat tres fluxos (mount points) amb diferents qualitats[cite: 174, 408]:

| Punt de Muntatge | Format | Bitrate | Descripció |
| :--- | :--- | :--- | :--- |
| `/radio-dgutierrez.mp3` | MP3 | 128 kbps | [cite_start]Qualitat estàndard[cite: 64, 102]. |
| `/radio-dgutierrez-hq.mp3` | MP3 | 320 kbps | [cite_start]Alta qualitat (HQ)[cite: 177, 181, 195]. |
| `/radio-dgutierrez.opus` | Opus | 96 kbps | [cite_start]Alta eficiència i qualitat excel·lent[cite: 411, 427, 437]. |

## 🚀 Funcionalitats Avançades

### 🔄 Playlist i Metadades
* [cite_start]**Playlist Rotativa:** Ús de fitxers `.txt` i la funció `concat` de FFmpeg per reproduir una llista de cançons en bucle[cite: 520, 521, 527, 529].
* [cite_start]**Metadades Dinàmiques:** S'ha configurat el paràmetre `-map-metadata 0` per enviar la informació de l'artista i títol en temps real[cite: 532, 533, 537].

### 📅 Programació Horària
[cite_start]S'utilitza un script de Bash (`radio_control.sh`) gestionat per **cron** per automatitzar l'emissió[cite: 541, 542, 544]:
* [cite_start]**08:00:** Inici de l'emissió matinal[cite: 584].
* [cite_start]**14:00:** Canvi a l'emissió de tarda[cite: 584].
* [cite_start]**22:00:** Aturada total del sistema per a la nit[cite: 562, 584].

## 📈 Càlculs d'Amplada de Banda
[cite_start]Per a una emissió de 128 kbps[cite: 496, 497]:
* [cite_start]**15 oients simultanis:** Requereixen 1,92 Mbps de pujada[cite: 499].
* [cite_start]**Capacitat màxima (10 Mbps):** Pot donar servei a uns 78 oients[cite: 500, 502, 503].
* [cite_start]**Consum de dades:** 10 oients constants durant 30 dies consumeixen aproximadament 414,72 GB[cite: 504, 511].

## 🔍 Resolució de Problemes
[cite_start]Si el streamer no es connecta, cal revisar[cite: 515, 516]:
1. [cite_start]Les credencials de la font en el fitxer XML i el comando FFmpeg[cite: 517].
2. [cite_start]La configuració del Host i el port en el fitxer de Docker[cite: 518].
3. [cite_start]La definició correcta dels punts de muntatge (Mount points)[cite: 519].

---
[cite_start]*Documentació generada a partir de l'entrega de Pràctica 1 de David Gutiérrez Navío.* [cite: 1, 2]
