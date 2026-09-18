# PymeTrazza (antes LogiFlow)

## Problema
Las pymes de LATAM que reparten a domicilio coordinan rutas, repartidores y avisos al cliente por WhatsApp y planillas: sin trazabilidad, sin estados y con el dueño encima de cada pedido.

## Qué construí
Un SaaS multi-tenant de logística de última milla: cada pyme tiene su espacio, sus pedidos, sus repartidores y el seguimiento de cada entrega. Modelo de datos, backend y despliegue propios, pensados para varias empresas sobre la misma instalación.

## Stack
Backend propio · base de datos relacional · despliegue en servidor Linux con Docker · separación estricta por tenant.

## Decisiones técnicas
- Multi-tenant desde el modelo de datos, no como parche: cada consulta está acotada al tenant.
- Despliegue reproducible con Docker para poder mover la instalación de servidor sin rehacer nada.
- Entrega incremental: primero una versión chica operativa, después las funciones que piden los usuarios reales.

## Qué aprendí
Que el aislamiento entre clientes se diseña el primer día o se paga después; y que un despliegue que se puede recrear desde cero vale más que cualquier optimización prematura.

## Estado
En desarrollo / lanzamiento en Chile. Código privado.
