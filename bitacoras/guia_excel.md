# Guía de Implementación en Excel para RCV

## 1. Fórmulas de Cálculo Automático

### Índice de Masa Corporal (IMC)
- **Celda A1:** Peso (kg)
- **Celda B1:** Talla (metros)
- **Fórmula:** `=A1/(B1^2)`

### Clasificación de Presión Arterial (AHA)
- **Celda C1:** Sistólica (PAS)
- **Fórmula:** `=SI(C1>=140;"Estadio 2";SI(C1>=130;"Estadio 1";SI(C1>=120;"Elevada";"Normal")))`

### Riesgo "Automático" (Lógica de Cribado)
- **Celda D1:** ¿Tiene Infarto/Ictus? (S/N)
- **Celda E1:** ¿DM con daño órgano blanco? (S/N)
- **Fórmula:** `=SI(O(D1="S";E1="S");"Muy Alto Riesgo";"Evaluar con Escala")`

## 2. Programación de Escalas (Estructura de Datos)

Para programar SCORE2 o ASCVD, se recomienda usar una tabla de referencia y la función `BUSCARV` o `INDICE/COINCIDIR`, ya que son fórmulas logarítmicas complejas:
- **Estructura:** `Riesgo = 1 - S0(t)^exp(Sum(Beta * (Valor - Media)))`
- **Recomendación Práctica:** Debido a la complejidad de las potencias y coeficientes Beta, se sugiere crear una pestaña oculta con los coeficientes por sexo y edad.

## 3. Semaforización (Formato Condicional)
- **Rojo:** Muy Alto Riesgo / TA >140/90.
- **Naranja:** Alto Riesgo.
- **Amarillo:** Riesgo Moderado.
- **Verde:** En Meta.
