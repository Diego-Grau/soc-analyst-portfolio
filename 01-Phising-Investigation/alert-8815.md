# Alerta 8815 – Phishing (Spoofing de Amazon – Correo Recibido)

## Detalles del Evento
- **Fecha/Hora:** 25/03/2026 08:37 UTC
- **ID de Alerta:** 8815
- **Prioridad:** Media

## Entidades Involucradas
- **Remitente:** urgents[@]amazon[.]biz
- **Destinatario:** h.harris[@]thetrydaily[.]thm (Hanna Harris)
- **URL Detectada:** hxxp://bit[.]ly/3sHkX3da12340
- **Asunto:** Acción Urgente Requerida - Problema con su cuenta de Amazon

## Hallazgos de la Investigación
- **Suplantación de Identidad (Spoofing):** El dominio `amazon[.]biz` no es oficial de Amazon; se usa TLD inusual para evadir filtros.
- **Uso de Acortadores de URL:** Se utiliza `bit[.]ly` para ocultar el destino final del enlace.
- **Ingeniería Social:** Mensaje con urgencia (“Action Required”) para inducir clic rápido.
- **Interacción del Usuario:** No hay evidencia de clic ni acceso a la URL. El correo solo fue recibido en el buzón.

## Veredicto
**True Positive (TP) – Correo Malicioso Detectado**  

## Evaluación de Impacto
- **Interacción del Usuario:** No realizada.  
- **Resultado de la Conexión:** Ninguno, el enlace no fue accedido.  
- **Riesgo Organizacional:** Exposición al intento de phishing; la cuenta de Hanna Harris no se considera comprometida.

## Decisión de Escalación
- Escalado a SOC L2 para seguimiento y concienciación interna.
- No se requiere intervención inmediata (L3).

## Acciones Recomendadas
1. Informar a Hanna Harris del correo malicioso recibido y reforzar la educación sobre phishing.  
2. Bloquear el dominio `amazon[.]biz` y la URL en el proxy/firewall.  
3. Registrar el evento en el SIEM y marcarlo como “Correo Malicioso – No interactuado”.  
4. Incluir este caso como ejemplo en campañas de concienciación interna.

## Evidencia Técnica
- Para consultar el evento de correo en Splunk:  
[Evidencia Técnica](splunk_queries.md)
