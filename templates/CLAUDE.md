<!-- PLANTILLA — cópiala a un archivo CLAUDE.md en la raíz de tu repo.
     Reemplaza los [placeholders] y borra lo que no aplique.
     Regla: SOLO lo estable. Lo repetible va en skills; lo determinístico en hooks. -->

# [Nombre del proyecto]

## Contexto

[Qué es en 1-3 frases y qué stack usa.] Para arquitectura y diagramas, ver README.md.

## Comandos

```bash
[setup]        # instalar / preparar entorno
[run]          # levantar en local
[test]         # correr tests
[lint]         # linter / formato
[deploy]       # desplegar (si aplica)
```

## Fuentes de verdad

- [Dónde vive la definición correcta: README, schema, contrato de API, documentación
  de arquitectura, semantic layer o métricas canónicas.]
- No inventes interfaces, supuestos o definiciones: consulta primero estas fuentes.

## Convenciones

- Estilo: [ej. type hints; snake_case en Python, camelCase en JS/TS].
- Estructura: [ej. un modelo por archivo en models/].
- [Otras convenciones del equipo.]

## Criterios de "done"

- [Qué debe cumplirse para dar algo por terminado: tests pasan, lint limpio,
  validado como usuario, CHANGELOG actualizado.]
- Prueba lo que haces (tests/logs/capturas); no reportes "funciona" sin evidencia.

## Seguridad y límites

- Secretos fuera del repo y del contexto. Preferir keychain o un gestor de secretos;
  usar `.env` sólo como alternativa local ignorada y mantener `.env.example` con
  placeholders. No imprimir secretos ni pasarlos como argumentos. Referencia:
  https://github.com/ronaldmego/claude-kit/blob/main/docs/security.md
- **Áreas off-limits (⚠️ NO TOCAR):** [fork externo, app hermana, código generado —
  márcalas para que el agente no edite lo que parece muerto pero no lo es].
- Acciones irreversibles (borrar, publicar, enviar, producción) requieren aprobación
  humana: el agente prepara, tú apruebas.
