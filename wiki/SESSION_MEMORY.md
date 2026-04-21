# Session Memory — Memoria Entre Sesiones

## Problema conocido

Sessions NO persisten memoria entre sesiones a pesar de lo que dicen los docs. Necesita investigacion y fix.

## Solucion temporal

Configurar umbrales agresivos de flush para que preferencias se retengan aunque sesiones sean breves o gateway se reinicie.

## Skills asociadas

- `hermes-session-recall-debugging`: "Debug and fix Hermes cases where cross-session memory fee..."
- `hermes-auto-session-recall-bootstrap`: "Implement and validate automatic recent-session context i..."

## SessionDB

- Ubicacion: `hermes_state.py`
- Usa SQLite con FTS5 para busqueda
- Metodo: `session_search` para buscar en conversaciones pasadas

## Notas de implementacion

- Aggressive memory settings: bajos thresholds de flush para preservar estado
- Cuando el gateway se reinicia, la sesion anterior debe ser recuperable
- Si algo falla en session recall: usar skill `hermes-session-recall-debugging`
