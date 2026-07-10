# ADR 003: Uso de Conventional Commits para el Registro de Commits

## Estado
Propuesto

## Contexto
En el ecosistema de desarrollo del LICA coexisten realidades muy diversas, con la participación de docentes, investigadores, becarios y estudiantes que cuentan con distintos niveles de dedicación y experiencia. A medida que los proyectos del laboratorio crecen y evolucionan, el historial de Git se vuelve una herramienta fundamental para comprender los cambios en el código base, facilitar la colaboración y permitir el rastreo histórico (backtracking).

Actualmente, los mensajes de commit no siguen un formato estandarizado, lo que en proyectos de mayor escala dificulta la legibilidad y la posible automatización de tareas. Si bien la adopción de una convención estricta resolvería este problema, es importante reconocer el nivel de madurez organizacional actual del LICA, donde aún nos encontramos consolidando prácticas fundamentales de desarrollo (tales como la documentación, la organización de repositorios y los criterios de ramas).

Imponer una norma obligatoria en este escenario conlleva el riesgo de generar fricción o de que la regla sea ignorada en la práctica. Por lo tanto, surge la necesidad de introducir un estándar reconocido, como **Conventional Commits**, pero desde un enfoque flexible. El objetivo es proporcionar una herramienta organizativa valiosa para aquellos proyectos piloto que ya cuentan con la estabilidad necesaria para aprovecharla, y al mismo tiempo, establecer una guía de referencia recomendada hacia la cual los demás equipos puedan evolucionar de forma natural y orgánica.

## Decisión
Se decide recomendar la adopción de la especificación **Conventional Commits 1.0.0** como una buena práctica dentro del LICA, e iniciar un proceso de adopción gradual a través de proyectos ya establecidos a modo piloto.

Para facilitar la transición y no sobrecargar a los equipos, se establecen las siguientes pautas:
1. **Adopción gradual y voluntaria**: El estándar no será una norma obligatoria de manera inmediata para la totalidad de los proyectos del laboratorio. Se implementará poco a poco en desarrollos que ya están en curso y con una trayectoria estable, o en aquellos equipos que deseen incorporar la práctica de forma voluntaria.
2. **Recomendación general**: Para los proyectos restantes, se sugiere su uso como una guía de buenas prácticas que ayuda a mantener el orden en el historial de Git.

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

## Asistente de IA (Prompt de Ayuda)
Para facilitar la adopción de esta convención, especialmente para quienes se están familiarizando con el formato, se sugiere utilizar el siguiente prompt con cualquier herramienta de Inteligencia Artificial (ChatGPT, Gemini, Claude, etc.) para redactar el mensaje de commit:

> [!TIP]
> **Prompt para copiar y pegar:**
> ```text
> Actúa como un asistente de desarrollo de software. Tu tarea es ayudarme a escribir un mensaje de commit que cumpla con la especificación de Conventional Commits 1.0.0 y las convenciones internas de nuestro laboratorio.
> 
> Convenciones a seguir:
> 1. Tipo (en inglés): Debe ser uno de los siguientes: feat, fix, docs, style, refactor, perf, test, build, ci, chore, enhancement.
> 2. Alcance (opcional): Indica el módulo, componente o área afectada entre paréntesis, ej: (auth), (api), (ui). Debe ser breve y en inglés o español según corresponda al código.
> 3. Descripción corta (en español): Debe comenzar con un verbo en infinitivo (ej: agregar, corregir, modificar, eliminar), redactada de forma concisa y enfocada en el "qué" cambia. No uses punto final.
> 4. Cuerpo (opcional): Explica el "por qué" del cambio y detalles de la solución, redactado en español. Sepáralo del título con una línea en blanco.
> 5. Pie de página (opcional): Si hay cambios importantes que rompen compatibilidad, deben indicarse con "BREAKING CHANGE:" o agregando un signo "!" después del tipo/alcance. Si se referencia a una tarea o PR, usa "Refs: #número".
> 
> Te proporcionaré la descripción informal de lo que hice o el diff de mis cambios. Tú debes devolver únicamente el mensaje de commit formateado listo para usar, y debajo una explicación muy breve (una sola oración) de por qué elegiste ese tipo y alcance si consideras que es necesario aclarar algo.
> 
> Aquí está lo que hice:
> [DESCRIBE AQUÍ TUS CAMBIOS DE MANERA INFORMAL O PEGA EL DIFF]
> ```

## Consecuencias
- **Positivas**:
  - **Trazabilidad y Backtracking**: Facilita enormemente el rastreo histórico de cuándo y por qué se introdujo un cambio específico.
  - **Legibilidad del Historial**: El historial de Git se vuelve uniforme y fácil de explorar por parte de desarrolladores actuales y futuros.
  - **Preparación para Automatizaciones**: Deja el repositorio listo para incorporar herramientas automáticas de integración continua, como generación de changelogs y análisis de commits.
  - **Versionado Semántico (SemVer)**: Permite inferir de forma sencilla el tipo de incremento de versión (`MAJOR.MINOR.PATCH`) basándose en el historial de commits.
- **Negativas**:
  - **Curva de Aprendizaje**: Requiere que los colaboradores, poco a poco, se adapten a las reglas y se familiaricen con la estructura correcta de los mensajes de commit (mitigado por el uso del Asistente de IA).
  - **Rigurosidad Adicional**: Añade un pequeño esfuerzo extra al momento de escribir commits, desincentivando commits rápidos y desorganizados (ej. "arreglos", "update").
  - **Corrección de Errores**: Si un commit se escribe de manera incorrecta, obliga al uso de `git commit --amend` o `git rebase -i` localmente antes de realizar la integración final.

## Planes de Futuras Herramientas y Automatización (Opcional y Progresivo)
Adoptar Conventional Commits sienta las bases para automatizar múltiples procesos.  
Sin embargo, estas integraciones **no se realizarán de manera inmediata ni generalizada**, sino que se evaluarán de forma progresiva en los proyectos que hayan adoptado este estándar, a medida que sus equipos maduren en la práctica:
1. **Linter de Commits**: Evaluar la implementación de herramientas como [commitlint](https://github.com/conventional-changelog/commitlint) o [gitlint](https://github.com/jorisroovers/gitlint) en githooks locales o pipelines de CI para validar automáticamente los commits, únicamente en proyectos piloto avanzados que así lo requieran.
2. **Generación Automática de Changelogs**: Utilizar herramientas como [git-cliff](https://git-cliff.org/) o [standard-version](https://github.com/conventional-changelog/standard-version) para compilar de manera automática un archivo `CHANGELOG.md` al liberar versiones, simplificando la comunicación de los cambios.

## Alternativas Consideradas
- **Mantener el estilo actual (estilo libre)**: Es una opción para proyectos iniciales, o nuevos miembros del laboratorio que aún no se han familiarizado con la convención. Sin embargo, se desaconseja su uso en proyectos con un historial de commits extenso o con múltiples colaboradores, ya que dificulta la trazabilidad y la automatización de procesos.

## Fecha
08/07/2026

## Autor
- [Caupolicán Ré](https://github.com/caupolicanre)

## Referencias
- [Conventional Commits v1.0.0 Specification](https://www.conventionalcommits.org/en/v1.0.0/)
- [Conventional Commits - About and Tooling](https://www.conventionalcommits.org/en/about/)
- [Semantic Versioning 2.0.0](https://semver.org/)
