# Git Flow Backend

Este repositorio usa tres ramas principales para organizar el desarrollo, validacion y despliegue del backend.

## Ramas principales

- `main`: rama estable. Solo recibe cambios aprobados desde `develop` mediante Pull Request.
- `develop`: rama de integracion. Aqui se unen las funcionalidades y correcciones antes de pasar a produccion.
- `deploy`: rama usada para preparar y ejecutar despliegues. Solo debe recibir cambios ya validados.

## Flujo de trabajo

1. Crear ramas de trabajo desde `develop`.
2. Nombrar ramas segun el tipo de cambio:
   - `feature/nombre-corto`
   - `fix/nombre-corto`
   - `docs/nombre-corto`
   - `chore/nombre-corto`
3. Abrir Pull Request hacia `develop`.
4. Validar build, pruebas y revision de codigo antes de aprobar.
5. Integrar `develop` hacia `main` cuando el backend este estable.
6. Integrar `main` hacia `deploy` cuando se prepare un despliegue.

## Politicas de Pull Request

- Todo cambio debe entrar por Pull Request.
- Cada Pull Request debe tener una descripcion breve del cambio y su impacto.
- No se deben mezclar cambios no relacionados en el mismo Pull Request.
- Antes de mergear, el proyecto debe compilar correctamente.
- Si existen pruebas automatizadas, deben ejecutarse y pasar.
- Los cambios de configuracion sensible no deben incluir secretos reales.

## Criterios minimos de validacion

- `mvn test` o comando equivalente ejecutado correctamente cuando aplique.
- Variables de entorno documentadas en `.env.example` si se agregan nuevas configuraciones.
- Endpoints nuevos o modificados documentados en el README o documentacion tecnica.
- Dockerfile y compose actualizados si cambia el proceso de ejecucion.

## Proteccion recomendada en GitHub

Configurar reglas de proteccion para `main` y `deploy`:

- Requerir Pull Request antes de mergear.
- Requerir al menos una aprobacion.
- Bloquear push directo.
- Requerir checks de CI cuando el pipeline este disponible.
- Mantener historial lineal si el equipo acuerda usar squash merge o rebase.
