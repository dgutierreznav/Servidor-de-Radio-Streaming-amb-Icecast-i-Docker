# Proyecto de Servidor de Streaming Icecast

[cite_start]Este proyecto consiste en la implementación de un servidor de radio por streaming utilizando **Icecast2** como servidor y **FFmpeg** como fuente de audio (streamer), gestionado íntegramente mediante contenedores **Docker**[cite: 18, 78, 80]. [cite_start]El sistema permite la emisión en múltiples formatos (MP3 y Opus) y calidades, incluyendo automatización de horarios y gestión de metadatos dinámicos[cite: 174, 408, 532, 541].

---

## Miembros del proyecto

- [cite_start][David Gutiérrez Navío](https://github.com/tu-usuario) [cite: 2]

---

## Tecnologías utilizadas

- [cite_start]**Icecast2**: Servidor de streaming multimedia[cite: 1].
- [cite_start]**Docker & Docker Compose**: Despliegue y orquestación de servicios[cite: 78, 80].
- [cite_start]**FFmpeg**: Herramienta para la codificación y envío del flujo de audio[cite: 95, 96].
- [cite_start]**Bash Scripting**: Scripts de control para la programación horaria[cite: 542, 544].
- [cite_start]**Cron**: Automatización de tareas del sistema[cite: 563, 582].
- [cite_start]**XML**: Configuración personalizada del servidor[cite: 19, 22].

---

## Requisitos previos

- [cite_start]**Docker** y **Docker Compose** instalados en el sistema[cite: 116, 210].
- [cite_start]Archivos de audio en formato **MP3** o **Opus** dentro del directorio correspondiente[cite: 15, 17].
- [cite_start]Estructura de directorios creada (`audio`, `config`, `logs`).

---

## Instrucciones para poner en marcha el proyecto

1. **Preparar la estructura de directorios**:
   [cite_start]Crea las carpetas necesarias para organizar la configuración, los audios y los registros[cite: 8]:
   ```bash
   mkdir -p ~/radio-dgutierrez/{config,audio,logs} [cite: 9, 11]
