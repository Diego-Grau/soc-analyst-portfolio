# Alerta 8817 – Phishing (Typosquatting Microsoft – Correo Recibido)

## Detalles del Evento
- **Fecha/Hora:** 25/03/2026 08:39 UTC
- **ID de Alerta:** 8817
- **Prioridad:** Media (Correo malicioso detectado)

## Entidades Involucradas
- **Remitente:** no-reply[@]m1crosoftsupport[.]co
- **Destinatario:** c.allen[@]thetrydaily[.]thm (C. Allen)
- **IP de Origen (Correo):** 102.89.222.143 (Lagos, Nigeria)
- **URL Detectada:** hxxps://m1crosoftsupport[.]co/login

## Hallazgos de la Investigación
- **Técnica de Typosquatting:** El remitente utiliza `m1crosoftsupport[.]co` (con “1” en lugar de “i”) para intentar engañar al usuario.
- **Correo Recibido:** El correo fue entregado correctamente al buzón de C. Allen.
- **Interacción del Usuario:** No hay evidencia de clic ni acceso a la URL.
- **Riesgo Técnico:** Bajo a moderado, exposición a phishing sin interacción.

## Veredicto
**True Positive (TP) – Correo Malicioso Detectado**  
**Confianza:** Alta

## Evaluación de Impacto
- **Interacción del Usuario:** No realizada.
- **Resultado de la Conexión:** Ninguno, el enlace no fue accedido.
- **Riesgo Organizacional:** Solo exposición al intento de phishing; la cuenta de C. Allen no se considera comprometida.

## Decisión de Escalación
- Escalado a SOC L2 para seguimiento y concienciación interna.
- No se requiere intervención inmediata.

## Acciones Recomendadas
1. Informar a C. Allen del correo malicioso recibido y reforzar la educación sobre phishing.
2. Bloquear el dominio `m1crosoftsupport[.]co` y la URL en el proxy/firewall.
3. Registrar el evento en el SIEM y marcarlo como “Correo Malicioso – No interactuado”.
4. Incluir este caso como ejemplo en campañas de concienciación interna.

## Evidencia Técnica
- Para consultar el evento de correo en Splunk:  
[Evidencia Técnica](splunk_queries.md)
