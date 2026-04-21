# Docker Setup — Hermes en VPS

## Estructura del contenedor

- **Entry point**: `/entrypoint.sh` + `/hermes.sh`
- `/hermes.sh` ejecuta `hermes` solo cuando `ttyd` lanza el shell, luego cae a `zsh` al salir
- **Problema conocido**: policy de restart de Docker NO reinicia el gateway si `ttyd` se mantiene vivo

## HERMES_HOME

- En el VPS Docker de Miguel: `/opt/data`
  - Archivos de gateway (PID, status) viven aqui
  - NO bajo `~/.hermes`
- En el host: datos/config bajo `/docker/claude-code-oju7/data/`

## Despliegues al runtime

```bash
# NO usar cp directo — usar docker cp/docker exec
docker cp local/file.sh <container>:/opt/data/
docker exec <container> /opt/data/file.sh
```

## Config set en Docker

- `hermes config set` puede serializar valores estructurados (ej. `toolsets`) como string YAML en vez de lista real
- Tras cambios de listas/nidos: **revisar el `config.yaml` crudo**, no solo `hermes config`
- Esto aplica al contenedor Docker de Miguel

## Archivos criticos

- `/entrypoint.sh` — entry point del contenedor
- `/hermes.sh` — script de lanzamiento
- `config.yaml` en `HERMES_HOME` — configuracion activa
