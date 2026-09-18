# Tienda Global Chile

## Problema
Vender por WhatsApp escala mal: cada cotización, confirmación y seguimiento es una conversación manual, y un agente con LLM "suelto" inventa precios o estados.

## Qué construí
Un e-commerce con agentes de venta por WhatsApp (n8n + LLM) que cotizan, confirman pedidos y hacen seguimiento; un gateway de WhatsApp propio; el storefront publicado en Cloudflare Pages y correo transaccional. Además, un banco de pruebas automatizado ("gym") que verifica el comportamiento del agente contra casos reales antes de cada despliegue.

## Stack
n8n · agentes con LLM · gateway de WhatsApp propio · Cloudflare Pages · correo transaccional · servidor Linux con Docker.

## Decisiones técnicas
- **El modelo conversa, el código decide**: precios, stock y estados de pedido los resuelve código determinista; el LLM solo redacta.
- Banco de pruebas automatizado como gate: ningún cambio en el agente llega a producción sin pasar los casos del gym.
- Gateway de WhatsApp propio para no depender de un proveedor intermedio.
- Datos y credenciales fuera del repo y fuera del contexto del modelo.

## Qué aprendí
Que la confiabilidad de un agente no sale del prompt sino del contorno: qué puede decidir, qué no, y una batería de casos que lo demuestre cada vez.

## Estado
En producción. Código privado.
