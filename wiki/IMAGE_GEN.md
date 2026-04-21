# Generacion de Imagenes — MiniMax

## Configuracion actual

- **MiniMax**: Proveedor primario para generacion de imagenes y TTS
- **FAL**: Proveedor fallback (NO usar a menos que FAL_KEY exista Y MiniMax falla)

## Problema conocido (CRITICO)

El codigo de `image_generation_tool.py` tiene FAL como primary y MiniMax como fallback, pero Miguel NO quiere FAL nunca.

**Solucion**: Invertir la logica — MiniMax como primary, FAL como fallback (solo si FAL_KEY existe Y MiniMax falla).

## Skill asociada

- `hermes-image-gen-minimax-direct`: "Bypass broken image_gen tool delegation — call MiniMax AP..."
- `hermes-docker-config-and-imagegen-pitfalls`: "Troubleshoot Hermes in Docker when config edits look corr..."

## Proveedor de TTS

- MiniMax es el unico provider de TTS
- MiniMax ya quedo activo en TTS e image_gen
- La personalidad quedo en `dali`

## Verificacion

Despues de cualquier cambio en la logica de image_gen, verificar:
1. `hermes config` muestra MiniMax como primary
2. El `config.yaml` crudo tiene la estructura correcta (no YAML serializado como string)
3. Test con `image_generate` funciona correctamente
