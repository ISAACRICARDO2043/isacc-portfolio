# repartidor-avisos

## Problema
Un repartidor en ruta no puede avisar a cada cliente cuándo llega ni responder "¿dónde viene mi pedido?" mientras maneja.

## Qué construí
Un agente de WhatsApp que avisa las entregas a los clientes de la ruta y responde solo las consultas habituales, dejando al repartidor fuera del chat.

## Stack
Bot de WhatsApp · automatización con n8n/Python · agente con LLM para las respuestas · servidor Linux con Docker.

## Decisiones técnicas
- Avisos disparados por el estado real de la ruta, no por el chat: el bot informa, no improvisa.
- Modo de prueba sin envíos reales para verificar el comportamiento antes de tocar a clientes.
- Respuestas acotadas a lo que el sistema sabe; lo demás se deriva a una persona.

## Qué aprendí
Que en mensajería con clientes finales el primer requisito es no molestar: cada mensaje automático tiene que justificarse con un evento real.

## Estado
En producción. Código privado.
