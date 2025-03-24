# ADR 002: Estructura de Repositorio para Docencia en Programación Avanzada

## Estado
Propuesto

## Contexto
El repositorio `FIUNER-LICA/pa-repositorio-practica-plantilla` está diseñado para facilitar la enseñanza y el desarrollo de Trabajos Prácticos (TPs) en la asignatura de Programación Avanzada. Su estructura sirve como plantilla para organizar los TPs desarrollados por los estudiantes. Su principal objetivo es que tanto docentes y alumnos cuenten con una estructura clara y coherente para las entregas y el seguimiento de los trabajos a lo largo del cursado.

## Decisión
Se decidió mantener una estructura de directorios que incluye:
- `TrabajoPractico_1`: Carpeta independiente destinada al desarrollo y almacenamiento del primer trabajo práctico. Internamente, contiene carpetas específicas para diferentes tipos de archivos relacionados con el TP.
A medida que avance el curso, se prevé que los alumnos incorporen nuevos directorios para los trabajos prácticos posteriores, siguiendo la nomenclatura `TrabajoPractico_2`, `TrabajoPractico_3` manteniendo la misma estructura interna propuesta. 

## Consecuencias
- **Positivas**:
  - Facilita la organización y el acceso al material relacionado con cada trabajo práctico.
  - Permite a los estudiantes ubicar y gestionar su código y documentación de manera estructurada.
  - Mejora la mantenibilidad y escalabilidad del repositorio conforme se incorporan nuevos trabajos prácticos.
- **Negativas**:
  - Puede requerir una curva de aprendizaje inicial para que los nuevos estudiantes comprendan la estructura.
  - Es necesario mantener la consistencia en la estructura de los directorios a medida que se agregan nuevos TPs.

## Alternativas Consideradas
Se consideró la posibilidad de no definir una estructura fija y permitir que los estudiantes organicen los archivos como prefieran. Sin embargo, esta alternativa fue rechazada debido a la posibilidad de generar confusión y dificultar la revisión y mantenimiento del código.

## Fecha
16 de diciembre de 2024

## Autores
- [Diana C. Vertiz del Valle] (https://github.com/DianaVertizdelValle)

## Referencias
- [Repositorio en GitHub](https://github.com/FIUNER-LICA/pa-repositorio-practica-plantilla)
