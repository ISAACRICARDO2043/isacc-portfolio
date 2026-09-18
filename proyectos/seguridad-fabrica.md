# seguridad-fabrica

## Problema
Un PC de desarrollo y un servidor Linux con varios servicios en producción, sin endurecimiento ni backups probados: cualquier incidente era irrecuperable.

## Qué construí
Endurecimiento de ambas máquinas: auditd para auditoría, rkhunter para detección, backups con restic cuya restauración se verifica (no solo "backup exit 0"), y gates de seguridad semanales que avisan por Telegram únicamente cuando algo está en rojo.

## Stack
Linux · auditd · rkhunter · restic · systemd timers · alertas por Telegram.

## Decisiones técnicas
- Un backup solo cuenta si se restauró y se contó contra un manifiesto.
- Alertar solo en rojo: un canal que avisa "todo bien" cada semana termina ignorado.
- Gates mecánicos con código de salida, no revisiones a ojo.

## Qué aprendí
Que la seguridad operable es la que se verifica sola: lo que no tiene un check automático, no existe.

## Estado
En mantenimiento (gate semanal activo). Código privado.
