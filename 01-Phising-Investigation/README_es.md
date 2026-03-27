# Investigación de Phishing – SOC Simulator

## Resumen
Este proyecto documenta la investigación de múltiples alertas de seguridad relacionadas con actividad de phishing dentro de un entorno SOC simulado proporcionado por TryHackMe.

El análisis se centra en identificar intentos de phishing, evaluar el impacto real mediante correlación de logs en Splunk y determinar las acciones de respuesta basadas en datos de correo, firewall y tráfico web.

---

## Objetivos
- Identificar intentos de phishing y distinguirlos de correos legítimos.
- Analizar indicadores como dominios de remitentes, URLs y direcciones IP.
- Correlacionar eventos de correo con logs de red para verificar la interacción del usuario.
- Evaluar el éxito o fallo de las medidas de control (Firewall/Filtros).
- Determinar requisitos de escalación y recomendar acciones de remediación.

---

## Resumen de Incidentes

| Alert ID | Tipo                   | Descripción                                      | Interacción               | Escalación        |
|----------|------------------------|--------------------------------------------------|---------------------------|------------------|
| 8814     | Falso Positivo         | Correo legítimo de onboarding                    | N/A                       | No               |
| 8815     | Phishing               | Correo malicioso (suplantación de Amazon)       | No confirmada             | Sí (L2)          |
| 8816     | Intento de Conexión    | Conexión bloqueada hacia URL sospechosa         | Sí (Bloqueo firewall)     | Sí (L2)          |
| 8817     | Campaña de Phishing    | Dominio typosquatting (suplantación Microsoft)  | No confirmada             | Sí (Urgente)     |

---

## Hallazgos Clave

### Técnicas de Phishing Identificadas
- Suplantación de dominio (`amazon[.]biz`)
- Typosquatting (`m1crosoftsupport[.]co`)
- Uso de acortadores de URL (`bit[.]ly`)
- Ingeniería social basada en urgencia y soporte técnico

---

### Correlación de Eventos y Actividad de Red

**Análisis de Clics / Conexiones:**  
- Alerta 8815: correo recibido, **no hay evidencia de clic** en la URL.  
- Alerta 8816: host 10.20.2.17 intentó acceder a la URL sospechosa; la conexión fue **bloqueada por el firewall**.  
- Alerta 8817: correo recibido, **sin evidencia de interacción con la URL**.

**Fallo de Detección:**  
- El dominio `m1crosoftsupport[.]co` no estaba categorizado como malicioso, pero no se tiene evidencia de que el usuario accediera a la página de login.

---

## Evaluación de Impacto
- Interacción del usuario: confirmada solo en el intento de conexión de 8816 (bloqueado).  
- Tráfico saliente: solo registrado en 8816 y bloqueado por firewall.  
- Compromiso de sistema: no se detectó descarga de malware ni exfiltración de datos; riesgo limitado a exposición a phishing.

---

## Lógica de Escalación
- No escalado: falsos positivos o sin interacción.  
- Prioridad media: conexiones a IOCs bloqueadas (8816).  
- Prioridad alta: conexiones permitidas a infraestructura maliciosa (ninguna confirmada).

---

## Acciones de Respuesta
- Bloqueo de dominios e IPs en el SIEM.  
- Revisión y educación de usuarios sobre phishing.  
- Eliminación masiva de correos sospechosos (purge).  
- Revisión de logs de autenticación para eventos inusuales.  
- Mejora de reglas de filtrado en firewall y proxy.

---

## Indicadores de Compromiso (IOCs)

**Dominios:**
- amazon[.]biz
- m1crosoftsupport[.]co
- bit[.]ly/3sHkX3da12340

**Direcciones IP:**
- 67.199.248.11
- 102.89.222.143
- 45.148.10.131

---

## Conclusión
La detección del correo es el primer paso del análisis.

La correlación en Splunk muestra que solo hubo **un intento de conexión bloqueado por firewall** (alerta 8816), mientras que los demás correos fueron recibidos pero no accedidos.  

Esto indica que, aunque no hay compromiso confirmado, el incidente refuerza la necesidad de educación y bloqueos preventivos en la infraestructura de seguridad.
