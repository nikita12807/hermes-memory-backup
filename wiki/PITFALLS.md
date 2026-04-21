# Problemas Conocidos y Soluciones

## 1. Image Generation: FAL vs MiniMax

**Problema**: `image_generation_tool.py` tiene FAL como primary y MiniMax como fallback, pero Miguel NO quiere FAL.

**Solucion**: Invertir la logica — MiniMax primary, FAL solo si FAL_KEY existe Y MiniMax falla.

## 2. Docker Config Set — Listas serializadas como YAML

**Problema**: `hermes config set` puede serializar valores estructurados (toolsets) como string YAML en vez de lista real.

**Solucion**: Tras cambios de listas/nidos, revisar `config.yaml` crudo, no solo `hermes config`.

## 3. Session Memory no persiste

**Problema**: Sessions no persisten memoria entre sesiones.

**Solucion**: Configurar flush thresholds agresivos. Si persiste: skill `hermes-session-recall-debugging`.

## 4. Gateway no reinicia si ttyd esta vivo

**Problema**: Docker restart policy no reinicia el gateway si ttyd se mantiene vivo.

**Solucion**: Verificar `/hermes.sh` y `/entrypoint.sh`. Reiniciar manualmente si necesario.

## 5. Path hardcodeados ~/.hermes

**Problema**: Codigo que hardcodea `~/.hermes` rompe con profiles.

**Solucion**: Usar `get_hermes_home()` para paths, `display_hermes_home()` para mensajes al usuario.

## 6. Sesiones de test escriben a ~/.hermes

**Problema**: Tests que escriben a `~/.hermes/` fallan en CI.

**Solucion**: Fixture `_isolate_hermes_home` en `tests/conftest.py` redirige HERMES_HOME a temp dir.

## 7. Cross-tool references en schemas

**Problema**: Tool schemas que mencionan otros tools por nombre causan alucinaciones.

**Solucion**: Agregar referencias dinamicamente en `get_tool_definitions()` en `model_tools.py`.
