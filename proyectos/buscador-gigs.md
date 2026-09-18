# buscador-gigs

## Problema
Buscar trabajo freelance de automatización a mano es lento y ruidoso: decenas de ofertas por día, la mayoría con requisitos que no encajan (inglés fluido, seniority, stacks ajenos), y cada postulación exige leer y redactar.

## Qué construí
Un radar que consulta 6 job boards por APIs públicas (Remotive, RemoteOK, WeWorkRemotely, GetOnBrd, Jobicy, Himalayas), filtra por skills, geo e idioma, deduplica, y para los mejores nuevos corre un triage con `claude -p` que decide si la oferta es apta y redacta la carta o propuesta. Lo apto llega a Telegram vía n8n para aprobar con un toque. Corre 5 veces al día en un servidor Linux con un timer de systemd.

## Stack
Python (solo stdlib) · `claude -p` con salida JSON estructurada · n8n (webhook → Telegram) · systemd user timer · tests de funciones puras.

## Decisiones técnicas
- Solo APIs públicas, sin login ni navegadores automatizados: cero riesgo de bloqueo y cero credenciales de terceros.
- El modelo no decide el precio: el rango orientativo sale de una tabla; el LLM solo puede citarlo.
- `DRY_RUN=1` obligatorio en gates: sin envíos, sin estado, sin invocar el modelo; el único envío real es el gate de producción.
- Cada gate tiene control negativo (token falso, test roto, archivo de entorno roto) para probar que se pone rojo.

## Qué aprendí
Que el valor no está en buscar más sino en descartar mejor: el triage estructurado convirtió un feed ruidoso en pocas ofertas realmente postulables.

## Estado
En producción. Código público: https://github.com/ISAACRICARDO2043/buscador-gigs
