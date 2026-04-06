# Proyecto de Servidor de Streaming Icecast

Este proyecto consiste en la implementación de un servidor de radio por streaming utilizando **Icecast2** como servidor y **FFmpeg** como fuente de audio (streamer), gestionado íntegramente mediante contenedores **Docker**. El sistema permite la emisión en múltiples formatos (MP3 y Opus) y calidades, incluyendo automatización de horarios y gestión de metadatos dinámicos.

---

## Autor

- [David Gutiérrez](https://davidgutierrez.es/)

---

## Tecnologías utilizadas

- **Icecast2**
- **Docker & Docker Compose**
- **FFmpeg**
- **Bash Scripting**
- **Cron**
- **XML**

---

## Requisitos previos

- **Docker** y **Docker Compose** instalados en el sistema
- Archivos de audio en formato **MP3** o **Opus** dentro del directorio correspondiente
- Estructura de directorios creada (`audio`, `config`, `logs`).

---

## Instrucciones para poner en marcha el proyecto

1. **Preparar la estructura de directorios:**

   - Crea las carpetas necesarias para organizar la configuración, los audios y los registros
     
      ```bash
      mkdir -p ~/radio-nombre/{config,audio,logs}

2. **Configurar las credenciales de acceso:**
   
   - Contraseña de Fuente (Source): ********
   - Contraseña de Administración: ********
   - Puerto de escucha: 8000

3. **Iniciar el despliegue:**

   - LEvanta el servidor y los streamers automáticamente con Docker Compose:

      ```bash
      docker-compose up -d

---

## Puntos de montaje y calidades
   - El servidor está configurado para ofrecer diferentes flujos según el ancho de banda y la calidad deseada:
     
| Punto de Montaje | Formato | Bitrate | Calidad |
| :--- | :--- | :--- | :--- |
| `/radio-dgutierrez.mp3` | MP3 | 128 kbps | ]Estándar |
| `/radio-dgutierrez-hq.mp3` | MP3 | 320 kbps | [cite_start]Muy Alta |
| `/radio-dgutierrez.opus` | Opus | 96 kbps | Excelente |

---

## Funcionalidades avanzadas

**Gestión de contenido y metadatos**
   - **Playlist Rotativa**:
      - Se utiliza un archivo `bucle.txt` y la función `concat` de FFmpeg para emitir una lista de canciones en bucle infinito
        
   - **Metadatos Dinámicos**:
     - Los streamers están configurados con el parámetro `-map-metadata 0` para enviar información de artista y título automáticamente al servidor

**Programación horaria (Automatización)**
   - Se utiliza un script de control (`radio_control.sh`) sincronizado con el sistema Crontab para gestionar las emisiones según la hora:
      - **08:00:** Inicia el stream principal de la mañana
      - **14:00:** Cambio a un flujo de diferente calidad (HQ u Opus) por la tarde
      - **22:00:** Cierre de emisión y parada de servicios para la noche
