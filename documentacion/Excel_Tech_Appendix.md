# Apéndice Técnico: Codificación de Escalas RCV en Excel

Este documento proporciona los coeficientes y la lógica matemática necesaria para programar las calculadoras de riesgo directamente en su hoja de Excel.

---

## 1. ESCALA ASCVD (Pooled Cohort Equations - ACC/AHA)

La fórmula general para calcular el riesgo a 10 años es:
**Riesgo = 1 - (S10 ^ EXP(Suma_Individual - Media_Poblacional))**

### Tabla de Coeficientes (Beta)

| Variable (X) | Mujer Blanca | Hombre Blanco | Mujer Negra | Hombre Negro |
| :--- | :---: | :---: | :---: | :---: |
| ln(Edad) | -29.799 | 12.344 | 17.114 | 2.469 |
| (ln(Edad))^2 | 4.884 | 0 | 0 | 0 |
| ln(Col. Total) | 13.540 | 11.853 | 0.940 | 0.302 |
| ln(Edad) * ln(CT) | -3.114 | -2.664 | 0 | 0 |
| ln(HDL) | -13.578 | -7.990 | -18.920 | -2.307 |
| ln(Edad) * ln(HDL) | 3.149 | 1.769 | 4.475 | 0 |
| ln(PAS) Tratada | 2.019 | 1.916 | 0.512 | 1.933 |
| ln(PAS) No Tratada | 1.957 | 1.764 | 0.454 | 1.864 |
| Fumador (Sí=1, No=0) | 7.574 | 7.837 | 0.691 | 0.630 |
| ln(Edad) * Fumador | -1.665 | -1.795 | 0 | 0 |
| Diabetes (Sí=1, No=0) | 0.661 | 0.658 | 0.874 | 0.845 |
| **Media (Sum_Mean)** | **-29.18** | **61.18** | **86.61** | **19.54** |
| **S10 (Basal)** | **0.9665** | **0.9144** | **0.9533** | **0.8954** |

### Ejemplo de Implementación en Excel
1. **Celdas de Entrada:** Edad (B1), ColTotal (B2), HDL (B3), PAS (B4), Tratada (B5: 1 o 0), Fuma (B6: 1 o 0), DM (B7: 1 o 0).
2. **Cálculo de Suma Individual (Mujer Blanca):**
   `= (-29.799 * LN(B1)) + (4.884 * (LN(B1))^2) + (13.54 * LN(B2)) + (-3.114 * LN(B1) * LN(B2)) + (-13.578 * LN(B3)) + (3.149 * LN(B1) * LN(B3)) + SI(B5=1; 2.019 * LN(B4); 1.957 * LN(B4)) + (7.574 * B6) + (-1.665 * LN(B1) * B6) + (0.661 * B7)`
3. **Resultado Final:**
   `= 1 - (0.9665 ^ EXP(Suma_Indiv - (-29.18)))`

---

## 2. ESCALA SCORE2 (ESC - Europea)

SCORE2 utiliza un modelo de riesgos competitivos que varía según la región (Europa de riesgo Bajo, Moderado, Alto y Muy Alto). La fórmula simplificada sigue el mismo principio que ASCVD pero con diferentes constantes.

### Variables SCORE2:
- Edad (40-69 años).
- Tabaquismo.
- PAS.
- Colesterol No-HDL (Col. Total - HDL).

### Lógica Sugerida para Excel:
Debido a que los coeficientes de SCORE2 dependen de la región geográfica, la forma más eficiente de programarlo es mediante una **Tabla de Referencia** en una pestaña oculta y usar la función `BUSCARV` para extraer el riesgo basado en los deciles de edad y niveles de No-HDL.

---

## 3. CONSEJOS DE PROGRAMACIÓN
- **Validación de Datos:** Use la herramienta "Validación de datos" para asegurar que la Edad esté entre 40 y 79 años (rango validado para estas escalas).
- **Protección de Celdas:** Bloquee las celdas que contienen las fórmulas matemáticas para evitar ediciones accidentales.
- **Visualización:** Multiplique el resultado final por 100 para obtener el valor en porcentaje (%).
