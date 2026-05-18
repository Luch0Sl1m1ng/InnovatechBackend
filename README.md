# Innovatech - EP2 Despliegue de Aplicaciones

## Información del Despliegue
* **IP Pública:** `3.80.103.181` 
* **URL Front-end:** `http://3.80.103.181:80`
* **Tecnologías:** React, Docker, AWS EC2, GitHub Actions.

## 🛠️ Configuración de Infraestructura
Se utilizó una instancia **EC2 (Amazon Linux 2023)** con las siguientes mejoras:
1. **Memoria Swap:** Se configuraron 2GB de Swap para evitar caídas del servidor por falta de RAM durante el despliegue.
2. **Docker:** Aplicación contenedorizada para asegurar la portabilidad.

## 🤖 Pipeline CI/CD
Se configuró un flujo de GitHub Actions para despliegue automatizado. 
*Nota: El pipeline presenta un error de autenticación con el host SSH, pero los scripts de despliegue están correctamente definidos en `.github/workflows/deploy.yml`.*
