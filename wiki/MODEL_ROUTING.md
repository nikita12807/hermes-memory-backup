# Model Routing — Estrategia de Enrutamiento

## Objetivo

Proteger GPT-5.4/Codex para trabajo mas demandante, usar modelos mas economicos para tareas simples, y configurar fallbacks cross-provider para rate limits.

## Configuracion actual

### Modelo primario

- **kimi-for-coding**: Establecido como PRIMARY en model routing (antes era secondary/fallback)

### Fallback provider

- **Z.AI / GLM**: `glm-5.1` configurado como backup
- **Base URL**: `https://api.z.ai/api/coding/paas/v4`
- **Uso**: Cuando OpenAI Codex rate limit golpea (ventana de 5hr, resetea a las 2:06 AM)

### Provider principal

- **OpenAI**: GPT-5.4 (Codex) como modelo premium
- **Fallback**: GLM-5.1 (Z.AI) cuando rate limit de Codex se agota

## Skill asociada

Ver: `hermes-cost-optimized-model-routing` — "Configure Hermes to minimize model cost by routing simple tasks through cheaper models"

## Archivos relevantes

- `hermes_cli/models.py` — catalogo de modelos, listas de providers
- `hermes_cli/model_switch.py` — pipeline compartido de `/model`
- `agent/models_dev.py` — registro de models.dev (provider-aware context)
- `hermes_cli/auth.py` — resolucion de credenciales de providers
