# EVCS Location Analyzer — Electrocentro S.A.

> **Sistema de evaluación y selección multicriterio de ubicaciones candidatas para estaciones de carga de vehículos eléctricos (EVCS).**

Implementación web completa y moderna del modelo metodológico:
$$\text{Excel} \longrightarrow \text{AHP} \longrightarrow \text{TOPSIS} \longrightarrow \text{Dijkstra} \longrightarrow \text{Puntaje Total (0--100)} \longrightarrow \text{p-mediana} \longrightarrow \text{Asignación y Cobertura}$$

---

## ⚡ Características Principales

1. **Ingesta y Carga de Red**:
   - Carga interactiva de libros Excel (`.xlsx`) con hojas `Nodos`, `Alimentadores`, `Lineas`, `Parametros`.
   - Incluye **Dataset Verificado de Electrocentro** (Salesianos, Huayucachi, Parque Industrial, Concepción, Xauxa).
   - Descarga de plantilla oficial en blanco lista para usar.
2. **Controles y Parámetros en Tiempo Real**:
   - Selector interactivo de número de EVCS a instalar ($p$).
   - Filtro de umbral de potencia de subestación (MVA).
   - Ponderación de factores con suma constante 100% ($w_{\text{topsis}} + w_{\text{dijkstra}} = 100\%$).
   - Modal interactivo de la Matriz de Comparación por Pares de Saaty (AHP) con cálculo en vivo de autovalor $\lambda_{\max}$, $CI$ y razón de consistencia $CR$.
3. **Claridad Metodológica Clave**:
   - Distingue con precisión entre el **Ranking Individual** (donde *SE Parque Industrial* es #1 con 66.07/100 por su óptima centralidad de red) y la **Selección de p-mediana** (*SE Salesianos + SE Xauxa*, 4.93 km de distancia media ponderada).
   - Incorpora el **Índice Global Integral de la Solución** que balancea la calidad técnica de las estaciones con la cobertura territorial efectiva.
4. **Visualización Gráfica**:
   - Diagrama topológico interactivo de la red de transmisión de 60 kV.
   - Resaltado visual con auras de las EVCS seleccionadas.
   - Rutas de asignación p-mediana en arcos punteados con distancias de atención.
   - Gráficos de barras para puntajes totales y comparativa TOPSIS vs Dijkstra.
5. **Exportación de Resultados**:
   - Descarga a Excel multihoja (`.xlsx`) con las 6 hojas de resultados (`Ranking_integral`, `EVCS_seleccionadas`, `Dijkstra`, `Asignaciones`, `Pesos_AHP`, `Resumen`).
   - Informe técnico para impresión / guardado en PDF con formato ejecutivo.

---

## 🚀 Ejecución Local

```bash
# 1. Instalar dependencias
npm install

# 2. Iniciar el servidor de desarrollo
npm run dev

# 3. Compilar para producción
npm run build
```

---

## ☁️ Despliegue en Vercel

Este proyecto cuenta con `vercel.json` preconfigurado para despliegue instantáneo:

1. **Vía GitHub / GitLab / Bitbucket**:
   - Sube este repositorio a tu cuenta de GitHub.
   - Ingresa a [Vercel](https://vercel.com) e importa el repositorio.
   - El framework `Vite` y el comando de build `npm run build` se detectarán automáticamente.
   - Haz clic en **Deploy**.

2. **Vía Vercel CLI**:
   ```bash
   npm i -g vercel
   vercel
   ```

---

## 📊 Estructura del Libro Excel de Entrada

| Hoja | Columnas Requeridas | Descripción |
|---|---|---|
| **Nodos** | `ID`, `Nombre`, `Tension_AT_kV`, `Potencia_MVA` | Subestaciones de potencia evaluadas |
| **Lineas** | `Linea`, `Extremo_A`, `Extremo_B`, `Longitud_km` | Tramos de líneas de transmisión eléctrica |
| **Alimentadores** | `Nodo_ID`, `Alimentador` | Alimentadores de media tensión (proxy de demanda) |
| **Parametros** | `Num_EVCS`, `Peso_TOPSIS`, `Peso_Dijkstra` | Parámetros iniciales de simulación |
