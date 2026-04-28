# Alerta 8816 – Intento de Conexión Maliciosa (Bloqueado)

## Detalles del Evento
- **Fecha/Hora:** 25/03/2026 08:38 UTC  
- **ID de Alerta:** 8816  
- **Prioridad:** Media-Alta  

---

## Entidades Involucradas
- **IP de Origen:** 10.20.2.17 (Hanna Harris - Endpoint)  
- **IP de Destino:** 67.199.248.11 (Asociada a Bitly / Infraestructura de Phishing)  
- **URL Detectada:** hxxp://bit[.]ly/3sHkX3da12340  
- **Herramienta de Detección:** TryDetectThis (IDS / Firewall)  

---

## Hallazgos de la Investigación
El análisis de los logs de tráfico de red en el SIEM revela una correlación directa con la campaña de phishing de Amazon (Alerta 8815):

- **Confirmación de Clic:**  
  El host 10.20.2.17 intentó realizar una petición HTTP hacia la URL acortada exactamente un minuto después de la llegada del correo malicioso. Esto confirma la interacción del usuario.

- **Acción del Firewall:**  
  La conexión fue interceptada y denegada exitosamente (Action: blocked) gracias a la regla de seguridad "Blocked Websites".

- **Análisis de Reputación:**  
  La IP de destino 67.199.248.11 ha sido reportada previamente en bases de datos de inteligencia de amenazas como parte de campañas de Credential Harvesting.

- **Estado del Host:**  
  No se observaron conexiones posteriores ni intentos de balizamiento (beaconing), lo que indica que el ataque fue contenido en la etapa de entrega.

---

## Veredicto
**True Positive (TP) – Intento de acceso a sitio de Phishing**  

---

## Evaluación de Impacto
- **Impacto en Seguridad:** Bajo (Mitigado). El firewall bloqueó el acceso al sitio de phishing.  
- **Riesgo Residual:** El usuario sigue siendo vulnerable a ingeniería social; se recomienda monitorización del endpoint para descartar descarga de archivos temporales antes del bloqueo.

---

## Decisión de Escalación
**Escalado a SOC L2**  
Se notifica para seguimiento del estado de seguridad del equipo de Hanna Harris y para reforzar las listas de bloqueo de DNS.

---

## Acciones Recomendadas
- Mantener la IP 67.199.248.11 en la lista negra global de la organización.  
- Realizar un escaneo rápido de malware en el host 10.20.2.17 como medida preventiva.  
- Incluir este incidente (anonimizado) como ejemplo en el próximo boletín de seguridad interna.  

---

## Evidencia Técnica
La consulta de Splunk que confirma este bloqueo y los detalles del log se encuentran en el [Evidencia Técnica](splunk_queries.md)
