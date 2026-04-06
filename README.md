# Proyecto de Servidor de Streaming Icecast

Este proyecto consiste en la implementación de un servidor de radio por streaming utilizando **Icecast2** como servidor y **FFmpeg** como fuente de audio (streamer), gestionado íntegramente mediante contenedores **Docker**. El sistema permite la emisión en múltiples formatos (MP3 y Opus) y calidades, incluyendo automatización de horarios y gestión de metadatos dinámicos.

---

## Autor

- [David Gutiérrez Navío](https://github.com/tu-usuario)

---

## Tecnologías utilizadas

- **Icecast2**: Servidor de streaming multimedia.
- **Docker & Docker Compose**: Despliegue y orquestación de servicios.
- **FFmpeg**: Herramienta para la codificación y envío del flujo de audio.
- **Bash Scripting**: Scripts de control para la programación horaria.
- **Cron**: Automatización de tareas del sistema.
- **XML**: Configuración personalizada del servidor.

---

## Requisitos previos

- **Docker** y **Docker Compose** instalados en el sistema.
- Archivos de audio en formato **MP3** o **Opus** dentro del directorio correspondiente.
- Estructura de directorios creada (`audio`, `config`, `logs`).

---

## Instrucciones para poner en marcha el proyecto

1. **Preparar la estructura de directorios:**
   Crea las carpetas necesarias para organizar la configuración, los audios y los registros:
   ```bash
   
   mkdir -p ~/radio-dgutierrez/{config,audio,logs}

2. **Configurar las credenciales de acceso:**
   
   - Contraseña de Fuente (Source): ********
   - Contraseña de Administración: ********
   - Puerto de escucha: 8000
