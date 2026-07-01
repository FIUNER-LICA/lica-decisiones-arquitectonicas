# ADR 003: Uso de Conventional Commits para el Registro de Commits

## Estado
Propuesto

## Contexto
En el desarrollo de software y la gestión de proyectos dentro de LICA, el historial de Git es una herramienta fundamental para comprender la evolución del código base, rastrear cambios (backtracking) y colaborar eficazmente. Actualmente, los mensajes de commit no siguen un formato estandarizado, lo que dificulta la legibilidad, la búsqueda histórica de cambios y la posibilidad de automatizar tareas relacionadas con el ciclo de vida del desarrollo.

Para resolver esto, se propone adoptar la especificación de **Conventional Commits**, la cual proporciona un conjunto de reglas sencillas para crear un historial de commits explícito y estructurado.

## Decisión
Se decide adoptar la especificación **Conventional Commits 1.0.0** para todos los mensajes de commit del proyecto.

La estructura de los mensajes de commit deberá ser:
```text
<tipo>[alcance opcional]: <descripción>

[cuerpo opcional]

[pie de página opcional]
```

### Tipos de commit obligatorios/estándar:
- **feat**: Incorpora una nueva funcionalidad al código base (correlacionado con `MINOR` en Semantic Versioning).
- **fix**: Corrige un error en el código base (correlacionado con `PATCH` en Semantic Versioning).

### Tipos adicionales recomendados (basados en la convención de Angular):
- **build**: Cambios que afectan el sistema de construcción o dependencias externas (ej. npm, maven, gradle).
- **ci**: Cambios en la configuración de integración y despliegue continuos (ej. GitHub Actions, Travis).
- **docs**: Modificaciones exclusivas en la documentación (ej. actualizar el archivo README o este ADR).
- **style**: Cambios estéticos o de formato que no afectan el comportamiento del código (espacios, punto y coma, etc.).
- **refactor**: Cambios en el código que no corrigen errores ni añaden funcionalidades (reestructuración del código).
- **perf**: Modificaciones de código destinadas a mejorar el rendimiento.
- **test**: Añadir o corregir pruebas existentes.
- **chore**: Tareas repetitivas o de mantenimiento general del repositorio que no modifican el código de producción.
- **enhancement**: Mejoras en funcionalidades existentes que no son nuevas características ni correcciones de errores.

### Cambios Importantes (BREAKING CHANGES):
Se representarán añadiendo un signo de exclamación `!` después del tipo/alcance (ej. `feat(api)!: eliminar endpoint deprecado`) o indicando explícitamente `BREAKING CHANGE:` en el pie de página del commit (correlacionado con `MAJOR` en Semantic Versioning).

## Directrices de Escritura y Idioma
Para garantizar la consistencia en el historial de cambios, se definen las siguientes reglas de redacción:
1. **Opcionalidad del cuerpo y pie**: El cuerpo y el pie de página son elementos completamente opcionales en la estructura de Conventional Commits. Solo deben utilizarse cuando aporten valor o contexto adicional relevante.
2. **Idioma estándar**: La redacción del mensaje del commit (descripción, cuerpo y pie) debe realizarse en el idioma que se utiliza en el proyecto, para mantener coherencia. Sin embargo, los **tipos de commits** (ej. `feat`, `fix`, `docs`, `refactor`, etc.) y la palabra clave `BREAKING CHANGE` en el pie de página deben escribirse en **inglés** tal cual están definidos en la especificación, garantizando que las herramientas automatizadas los reconozcan.
3. **Acción en infinitivo y enfoque en el "Qué"**: La descripción corta debe comenzar siempre con un verbo en infinitivo (por ejemplo: *agregar*, *corregir*, *eliminar*, *modificar*, *refactorizar*, o sus equivalentes en el idioma del proyecto) y debe detallar concretamente **qué** cambia en el commit (evitando explicar el "por qué" en este espacio).
4. **Explicación del "Por qué" en el cuerpo**: Si es necesario justificar o explicar los motivos o razones del cambio, esta información debe ubicarse en el **cuerpo** del commit, dejando la descripción breve y directa.
5. **Referencias en el pie de página**: Si el commit está relacionado con un issue, pull request o cualquier otro recurso externo, se debe incluir una referencia en el **pie de página** del commit (por ejemplo: `Refs: #45`), para mantener la trazabilidad y facilitar la navegación entre los cambios y sus contextos.

### Ejemplo Completo de Commit
A continuación se muestra un ejemplo de cómo debe estructurarse un commit completo bajo estas pautas:

```text
feat(auth): agregar modulo de inicio de sesión con JWT

Se implementa la autenticación mediante JSON Web Tokens (JWT) para asegurar las rutas privadas de la API del proyecto. Esto resuelve el problema de persistencia de sesión en entornos distribuidos.

Refs: #45
```

En este ejemplo:
- `feat` es el tipo (en inglés) y `(auth)` es el alcance.
- `agregar modulo de inicio de sesión con JWT` es la descripción corta, comenzando con un verbo en infinitivo y redactada en español, indicando **qué** cambia.
- El cuerpo (opcional) explica el **por qué** y detalles de la solución en español.
- El pie de página `Refs: #45` (opcional) relaciona el commit con un issue o pull request.

## Consecuencias
- **Positivas**:
  - **Trazabilidad y Backtracking**: Facilita enormemente el rastreo histórico de cuándo y por qué se introdujo un cambio específico.
  - **Legibilidad del Historial**: El historial de Git se vuelve uniforme y fácil de explorar por parte de desarrolladores actuales y futuros.
  - **Preparación para Automatizaciones**: Deja el repositorio listo para incorporar herramientas automáticas de integración continua, como generación de changelogs y análisis de commits.
  - **Versionado Semántico (SemVer)**: Permite inferir de forma sencilla el tipo de incremento de versión (`MAJOR.MINOR.PATCH`) basándose en el historial de commits.
- **Negativas**:
  - **Curva de Aprendizaje**: Requiere que los colaboradores se adapten a las reglas y se familiaricen con la estructura correcta de los mensajes de commit.
  - **Rigurosidad Adicional**: Añade un pequeño esfuerzo extra al momento de escribir commits, desincentivando commits rápidos y desorganizados (ej. "arreglos", "update").
  - **Corrección de Errores**: Si un commit se escribe de manera incorrecta, obliga al uso de `git commit --amend` o `git rebase -i` localmente antes de realizar la integración final.

## Planes de Futuras Herramientas y Automatización
Adoptar Conventional Commits sienta las bases para automatizar múltiples procesos en el futuro. Se contemplan las siguientes integraciones a mediano/largo plazo:
1. **Linter de Commits**: Implementar herramientas como [commitlint](https://github.com/conventional-changelog/commitlint) o [gitlint](https://github.com/jorisroovers/gitlint) en githooks locales o pipelines de CI para validar automáticamente la estructura de los commits antes de que sean aceptados.
2. **Generación Automática de Changelogs**: Utilizar herramientas como [git-cliff](https://git-cliff.org/) o [standard-version](https://github.com/conventional-changelog/standard-version) para compilar y documentar de manera automática todas las novedades, correcciones y cambios de impacto de forma estructurada en un archivo `CHANGELOG.md` al liberar una nueva versión.
3. **Automatización de Releases**: Implementar [semantic-release](https://github.com/semantic-release/semantic-release) para gestionar todo el flujo de publicación, cálculo del número de versión y publicación del paquete de forma 100% automatizada.

## Alternativas Consideradas
- **Mantener el estilo actual (estilo libre)**: Se rechazó debido a que la inconsistencia en los mensajes dificulta la automatización del ciclo de vida del software y hace que el historial de Git sea difícil de auditar a medida que el proyecto y los colaboradores crecen.

## Fecha
01/07/2026

## Autores
- [caupolicanre](https://github.com/caupolicanre)

## Referencias
- [Conventional Commits v1.0.0 Specification](https://www.conventionalcommits.org/en/v1.0.0/)
- [Conventional Commits - About and Tooling](https://www.conventionalcommits.org/en/about/)
- [Semantic Versioning 2.0.0](https://semver.org/)
