# DSC3_Proyecto
Este repositorio contiene la información necesaria para el trabajo desarrollado en el marco del proyecto final de Data Science 3 Coder House Noviembre 2026

# Librerías requeridas
# Python 3.13.18
scikit-learn==1.6.1
pandas==2.2.3
numpy==2.4.6
spacy==3.8.18
matplotlib==3.10.0
tqdm==4.67.3
# Modelo de SpaCy (se instala aparte): python -m spacy download en_core_web_sm
# Versión usada: core_web_sm 3.8.0

## Elección del modelo: regresión logística

Se elige regresión logística como clasificador de referencia (baseline) por lo siguiente:

1. **Es adecuada para este tipo de datos.** La matriz TF-IDF es esparsa y de alta
   dimensión (8.000 x 5.000, con densidad de 0,54%). Los modelos lineales como la
   regresión logística se usan de forma estándar en este escenario y entrenan rápido
   (la grilla de 24 configuraciones con 5 particiones cada una corrió en pocos minutos).
2. **Es interpretable.** Cada palabra tiene un coeficiente por clase. Esto permitió
   listar los términos más pesados de cada categoría y verificar que el modelo decide
   sobre todo por contenido temático (por ejemplo `nasa` y `microsoft` en Sci_Tech,
   `coach` y `league` en Sports), y detectar una firma de agencia (`afp`) entre los
   términos de World.
3. **Maneja bien varias clases** (clasificación multiclase con 4 categorías) y es un
   punto de partida habitual, con pocos hiperparámetros que ajustar.

Frente a las alternativas: Naive Bayes es aún más rápido, pero supone que las palabras
son independientes entre sí; las SVM lineales suelen rendir de forma parecida en texto
y también tienen coeficientes interpretables.

**Limitación:** en este trabajo no se comparó empíricamente los tres modelos, por lo que
no se puede afirmar que la regresión logística sea la mejor opción; se eligió como
referencia simple e interpretable. 

## Análisis preliminar matriz confusión
•	Business y Sci_Tech son el par más confundido: 83 de los 205 errores (el 40%) son entre ellas. Eso confirma la hipótesis de que son categorías con las palabras más específicas.
•	Sports casi no se confunde: solo 19 de sus 500 documentos se clasificaron mal.
