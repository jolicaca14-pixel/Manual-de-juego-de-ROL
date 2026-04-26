# Análisis de Arquitectura del Sistema - Manual RCV

## Objetivos de Expertise
Para cumplir con los `Objetivos.md`, el sistema requiere integrar las siguientes áreas:

1. **Cardiología Clínica:** Basada en guías AHA 2024 y ESC 2023. Enfoque en estratificación de riesgo (SCORE2, ASCVD Risk Estimator) y guías farmacológicas.
2. **Nutrición Clínica:** Protocolos de dieta DASH, mediterránea y manejo de dislipidemias.
3. **Psicología de la Salud:** Técnicas de entrevista motivacional y cambio de hábitos.
4. **Medicina Interna:** Manejo integral de diabetes, hipertensión y obesidad como co-factores de RCV.

## Diseño de Equipo (Agentes)

| Agente | Rol | Responsabilidad Principal |
| :--- | :--- | :--- |
| **CardioAgente** | Especialista RCV | Catalogación, estratificación y algoritmos farmacológicos. |
| **NutriAgente** | Nutricionista Clínico | Protocolos nutricionales específicos para hipertensión y dislipidemia. |
| **PsicoAgente** | Psicólogo Conductual | Protocolos de adherencia y manejo de estrés. |
| **EditorAgente** | Especialista en Documentación | Formateo Markdown, coherencia y estilo del entregable .txt. |

## Flujo de Trabajo
1. `CardioAgente` genera la estructura base y algoritmos médicos.
2. `NutriAgente` y `PsicoAgente` insertan sus secciones transversales.
3. `EditorAgente` valida el formato Markdown y la claridad técnica.
