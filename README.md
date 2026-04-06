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

```
radio-dgutierrez/
├── /audio
├── /config
├── /logs
├── docker-compose.yml
└── radio_control.sh
```

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
| `/radio-nombre_radio.mp3` | MP3 | 128 kbps | Estándar |
| `/radio-nombre_radio-hq.mp3` | MP3 | 320 kbps | Muy Alta |
| `/radio-nombre_radio.opus` | Opus | 96 kbps | Excelente |

---

## Funcionalidades avanzadas

**Gestión de contenido y metadatos**
   - **Playlist Rotativa**:
      - Se utiliza un archivo `bucle.txt` y la función `concat` de FFmpeg para emitir una lista de canciones en bucle infinito
        
   - **Metadatos Dinámicos**:
     - Los streamers están configurados con el parámetro `-map-metadata 0` para enviar información de artista y título automáticamente al servidor

**Programación horaria (Automatización)**
   - Se utiliza un script de control (`radio_control.sh`) sincronizado con el sistema Crontab para gestionar las emisiones según la hora:
      - **08:00** → Inicia el stream principal de la mañana
      - **14:00** → Cambio a un flujo de diferente calidad
      - **22:00** → Cierre de emisión y parada de servicios

---

## Acceso al proyecto

**Una vez los contenedores estén en marcha, puedes acceder a las siguientes URLs**:
   - **Panel de Administración**:

     ```bash
     http://localhost:8000/admin/

   - **Estado Público del Servidor**:

     ```bash
     http://localhost:8000/status.xsl

   - **Escuchar el Stream (MP3)**:

     ```bash
     http://localhost:8000/radio-nombre_radio.mp3

## Notas y recomendaciones

   - El ancho de banda de subida necesario se calcula multiplicando el bitrate del stream por el número de oyentes simultáneos
   - Los fallos de conexión suelen deberse a errores en las contraseñas, puertos incorrectos o puntos de montaje duplicados
   - La revisión de los archivos de registro es esencial para identificar errores de acceso y problemas de configuración en el servidor
