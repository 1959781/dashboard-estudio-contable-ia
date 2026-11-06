#Tablero de Control Visual Inteligente para Estudio Contable

Trabajo Final Integrador · Diplomatura en IA Aplicada a Entornos Digitales de Gestión · FCE-UBA · Cohorte 2026
Autora: Mónica A. Zeballos

## Ver el tablero en vivo

**https://monizeta2026.app.n8n.cloud/webhook/tablero-auditoria**

Se abre con cualquier navegador (también en el celular), sin usuario ni contraseña. Trabaja solo con datos ficticios.

## Qué hace

Responde la pregunta "¿cómo vamos?" del estudio contable. Lee el Excel maestro del equipo (OneDrive), audita los registros con IA y muestra el avance de cada área en un tablero con el "Efecto Vaso": la carga pendiente baja del 100 % (rojo) al 0 % (verde).

## Para qué sirve

- Detectar a tiempo los errores de carga del personal junior, antes de los vencimientos (ARCA, AGIP, ARBA, SIFERE).
- Ver en segundos el estado de Impuestos, Legales, Sueldos, Balances e Inspecciones.
- Reducir las consultas por WhatsApp y correo.

## Cómo se usa

1. El equipo carga su trabajo como siempre en el Excel `auditoria_contable_junior.xlsx`.
2. El Flujo #1 corre solo 3 veces por día (9, 13 y 18 h): oculta datos sensibles, consulta a Claude Haiku y guarda el diagnóstico en la pestaña "histórico".
3. Cualquier persona abre el link del tablero y ve el estado actualizado.

Códigos de estado: 3 = Pendiente (rojo) · 2 = En proceso (amarillo) · 1 = Completado (verde).

## Herramientas de IA y tecnología usadas

| Parte | Herramienta |
|---|---|
| Orquestación de flujos | n8n Cloud |
| Auditoría de registros | Claude Haiku (Anthropic), nodo nativo de n8n |
| Diseño y armado de los flujos y del tablero | Asistente de IA de n8n (codiseño) |
| Datos | Microsoft Excel en OneDrive (OAuth2) |
| Tablero web | HTML/SVG generado por un nodo Code y servido por un Webhook de n8n |

## Arquitectura

- **Flujo #1 – Auditoría Contable y Sanitización:** Schedule → Excel → Code (sanitización: [OCULTO], [CUIT], [EMAIL]) → Claude Haiku → Excel (histórico).
- **Flujo #2 – Servidor Web App del Tablero:** Webhook → lectura de 8 hojas del Excel → Code (arma el tablero) → Respond to Webhook (página HTML).

## Privacidad

- Datos 100 % ficticios en la demo.
- Claves fiscales reemplazadas por [OCULTO] y CUIT/DNI/CBU/emails enmascarados antes de enviar nada a la IA.
- El tablero es de acceso público solo para la evaluación académica; en uso real se recomienda volver a protegerlo con contraseña.

## Contenido del repositorio

| Archivo | Descripción |
|---|---|
| `README.md` | Este documento |
| `Informe_Trabajo_Final_Zeballos.pdf` | Informe escrito |
| `flujos/` | Exportación JSON de los flujos de n8n |
