# Alerta 8814 – Falso Positivo (Proceso de Onboarding)

## Detalles del Evento
- **Fecha/Hora:** 25/03/2026 08:34 UTC  
- **ID de Alerta:** 8814  
- **Prioridad:** Baja  

---

## Entidades Involucradas
- **Remitente:** onboarding@hrconnex.thm  
- **Destinatario:** j.garcia@thetrydaily.thm (Julia García)  
- **URL Detectada:** https://hrconnex.thm/onboarding/15400654060/j.garcia  
- **IP de Origen:** Interna (Red Corporativa)  

---

## Hallazgos de la Investigación
Tras analizar el correo electrónico y los logs asociados en el SIEM, se determinaron los siguientes puntos:

- **Verificación del Dominio:**  
  El dominio del remitente (hrconnex.thm) pertenece a la infraestructura interna de Recursos Humanos de la organización.

- **Análisis del Contenido:**  
  El cuerpo del mensaje es consistente con un procedimiento estándar de alta de nuevos empleados (onboarding).

- **Validación de URL:**  
  La estructura de la URL no presenta patrones de ofuscación ni técnicas de redirección maliciosas. Apunta a un servidor interno legítimo.

- **Contexto del Usuario:**  
  Se confirmó que Julia García es una nueva incorporación en la plantilla, lo que justifica la recepción de este tipo de comunicaciones.

---

## Veredicto
**Falso Positivo (FP) – Correo Legítimo**  

---

## Evaluación de Impacto
- **Impacto en Seguridad:** Nulo  
- **Acción del Firewall:** No se registraron bloqueos, ya que la comunicación es interna y segura  

---

## Decisión de Escalación
**No Escalado**  
La alerta se cierra como actividad legítima.

---

## Acciones Recomendadas
- Cerrar la alerta en el sistema de gestión de incidentes  
- **Tuning del SIEM (Opcional):** Ajustar la regla de detección para el dominio `hrconnex.thm` para evitar falsos positivos en futuros procesos de onboarding  
