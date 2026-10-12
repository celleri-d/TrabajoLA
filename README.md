# Radar Tutor UC

Trabajo aplicativo de Ciencia de Datos, Unidad 2 (Learning Analytics), Universidad de Cuenca.

Proponemos una herramienta de alerta temprana para que el tutor académico de primer ciclo sepa, desde la semana 4 del ciclo, a qué estudiantes conviene contactar primero. Combina la actividad en eVirtual con datos del sistema académico y registra cada intervención para poder evaluar después si sirvió.

## Canvas de diseño

| Bloque | Contenido |
|---|---|
| **1. Actor y decisión** | El tutor académico de primer ciclo. Cada semana decide a qué estudiantes llamar a tutoría, a cuáles escribirles con recursos y a cuáles derivar a Bienestar Universitario. Hoy lo hace casi siempre después del primer parcial (semanas 7–8), con la nota parcial o porque el estudiante lo busca. |
| **2. Problema educativo** | En la cohorte de la UCuenca que ingresó en marzo de 2013 (1 900 estudiantes), la reprobación fue la más alta en el primer año (12,8 %) y el abandono llegó al 6,8 % en el primer semestre y al 11,3 % en el primer año (Bravo, Peña e Illescas, 2020). Afecta a los estudiantes de primer ciclo y a sus tutores. |
| **3. Pregunta analítica** | *¿Qué estudiantes de un curso tienen alta probabilidad de reprobar o abandonar la asignatura, según su actividad en eVirtual y sus entregas durante las cuatro primeras semanas?* Nivel: predictiva. Tipo: enseñanza. |
| **4. Datos e indicadores** | eVirtual (clics, entregas, notas), sistema académico (matrícula, veces cursada, créditos, resultado final) y los registros de la herramienta. Indicador central I5: probabilidad de riesgo con regresión logística sobre I1 (clics de la semana / mediana del curso), I2 (días activos), I3 (entrega pendiente) e I6 (veces cursada y créditos). Semáforo: rojo ≥ 0,60; amarillo 0,40–0,60; verde < 0,40. |
| **5. Intervención** | Rojo: tutoría individual en 7 días o menos. Amarillo: mensaje con recursos (envío masivo con plantilla). Ambos pueden derivar a Bienestar y todo queda registrado (I7). Si no se actúa, el estudiante sigue sin apoyo hasta el primer parcial y aparece como *sin atender*. |
| **6. Ética y privacidad** | Seudónimos; el nombre solo lo ve el tutor asignado. Las variables demográficas no entran al modelo y solo se usan para revisar sesgos. Consentimiento informado con opción de retirarse (LOPDP, 2021). El estudiante no ve su probabilidad de riesgo. Contamos días activos y no horas para no perjudicar a quien trabaja. |
| **7. Prueba de concepto** | Dataset OULAD (22 cursos, 28 785 estudiantes). Calculamos I1–I4, I6 e I5 al día 28. Entrenando con 2013 y probando con 2014: AUC 0,72; con la alerta amplia, recall 0,82 y precisión 0,54. El notebook construye las cuatro pantallas de los wireframes con esos datos. Limitaciones: no son datos de la UCuenca y no demuestra impacto. |
| **8. Validación** | Hipótesis: entre los estudiantes alertados en la semana 4, la aprobación es mayor en los paralelos cuyo tutor usa la herramienta. Asignación aleatoria por paralelo durante un semestre. Criterios: AUC ≥ 0,70 y recall ≥ 0,75; SUS ≥ 68; 80 % de los rojos atendidos a tiempo. |
| **9. Preguntas abiertas** | ¿Una diferencia de aprobación entre grupos es real o es azar? ¿Cuántos paralelos necesitamos? ¿Qué prueba usamos con aprobado / no aprobado? ¿Cómo calculamos intervalos de confianza para el recall y el AUC? ¿La diferencia de recall por edad es significativa? |

La versión completa del Canvas está en [01_canvas/Canvas_diseno.pdf](01_canvas/Canvas_diseno.pdf).

## Entregables

| Fase | Entregable | Archivo |
|---|---|---|
| 0 | Matriz de análisis de casos (5 herramientas) | [00_analisis_casos/Matriz_analisis_casos.pdf](00_analisis_casos/Matriz_analisis_casos.pdf) |
| 1 | Canvas de diseño | Este README y [01_canvas/Canvas_diseno.pdf](01_canvas/Canvas_diseno.pdf) |
| 2 | Diccionario de datos, ética y privacidad | [02_datos/Diccionario_de_datos.pdf](02_datos/Diccionario_de_datos.pdf) |
| 3 | Wireframes, flujo de intervención y arquitectura | [03_diseno/Diseno_herramienta.pdf](03_diseno/Diseno_herramienta.pdf) |
| 4 | Notebook de prueba de concepto | [04_prueba_concepto/poc_radar_tutor.ipynb](04_prueba_concepto/poc_radar_tutor.ipynb) |
| 5 | Pitch de 6 minutos | [05_presentacion/Pitch.pdf](05_presentacion/Pitch.pdf) |
| 6 | Plan de validación | [06_validacion/Plan_de_validacion.pdf](06_validacion/Plan_de_validacion.pdf) |
| – | Declaración de uso de IA | [Declaracion_uso_IA.pdf](Declaracion_uso_IA.pdf) |

Los documentos están escritos en LaTeX y junto a cada PDF está su archivo `.tex`. Se compilan con `pdflatex`, excepto el pitch, que usa `xelatex` (fuente Open Sans).

## Cómo ejecutar el notebook

```bash
pip install -r 04_prueba_concepto/requirements.txt
cd 04_prueba_concepto
jupyter notebook poc_radar_tutor.ipynb
```

La primera vez el notebook descarga OULAD (unos 45 MB) en `data/`; esa carpeta no se sube al repositorio.
