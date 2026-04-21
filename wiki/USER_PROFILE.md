# Perfil del Usuario — Miguel Vera

## Identidad

- **Nombre**: Miguel Vera
- **Agente**: Hermes con personalidad "Dali" (inspirada en John Daly — excéntrico, muy seguro, excelente en lo que hace)
- **Idioma**: Español (preferido — respuestas breves y directas)
- **Plataforma**: Docker VPS con runtime de Telegram

## Preferencias de comunicacion

- Respuestas breves y directas en español
- No enumerar llamadas a herramientas salvo las absolutamente necesarias
- En tareas largas: updates breves y reales, no toleraba silencios
- Quiere que se le diga cuando algo no funciona tecnicamente en vez de inventar soluciones
- Prefiere comandos en bloques fÃ¡ciles de copiar ("celdas copy")
- Siempre cerrar la respuesta claramente sin dejarla colgando

## Preferencias tecnicas

- **Memoria persistente**: Prioriza continuidad sobre ahorro de API en chats cortos; prefiere umbrales agresivos de flush para que preferencias se retengan aunque las sesiones sean breves o el gateway se reinicie
- **Backups**: Siempre hacer backup antes de modificar scripts de startup/config en Docker
- **Model routing**: Quiere proteger GPT-5.4 para el trabajo mas demandante; usar kimi-for-coding para tareas intermedias; cross-provider fallbacks para rate limits

## Configuracion de providers

- **Primary model**: kimi-for-coding (antes era secondary/fallback)
- **Backup/Z.AI/GLM**: glm-5.1 como fallback cuando OpenAI Codex rate limit golpea
- **Ventana de rate limit Codex**: 5hr, se resetea a las 2:06 AM

## Configuracion de plataforma

- Docker Hermes en VPS
- Runtime de Telegram corre dentro del contenedor en `/opt/hermes` con `HERMES_HOME=/opt/data`
- En el host, datos/config bajo `/docker/claude-code-oju7/data/`
- Despliegues al runtime requieren `docker cp`/`docker exec`, no `cp` directo
