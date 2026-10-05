# ADR 004: Uso de Semantic Versioning para el Versionado de Proyectos

## Estado
Propuesto

## Contexto
A medida que un proyecto crece, se hace cada vez más importante gestionar de manera clara, predecible y uniforme las versiones de sus entregas. Al utilizar diferentes sistemas interconectados y librerías propias, los cambios de código o en las APIs (ya sean nuevas características, corrección de errores, o cambios incompatibles) pueden romper dependencias si no se comunican adecuadamente.

Actualmente, no hay definido un esquema estructurado de versionado formal en nuestro flujo de trabajo, y podría dificultar que los colaboradores/usuarios sepan si una nueva versión es segura para actualizarse o si introducirá cambios disruptivos (breaking changes) en el uso.

Aprovechando que ya se adoptó un formato para [Conventional Commits (ADR 003)](adr-003-usar-conventional-commits.md), es el paso natural adoptar una convención que se integre y refleje este ciclo de vida de los cambios en los números de las versiones (releases).

## Decisión
Se decide adoptar el estándar **[Semantic Versioning](https://semver.org/)** (SemVer), en su [versión 2.0.0](https://semver.org/spec/v2.0.0.html), como estrategia unificada para el versionado de sistemas y proyectos que se desarrollen en el LICA.

La adopción de esta estrategia conlleva el siguiente flujo de trabajo:
1. **Versionado MAJOR.MINOR.PATCH:**
   - **MAJOR**: Cambios incompatibles en la API o funcionalidad (incluyen un breaking change).
   - **MINOR**: Nuevas funcionalidades compatibles hacia atrás.
   - **PATCH**: Corrección de errores compatibles hacia atrás.
2. **Hitos y Tags (Milestones & Tags):**
   - Cada vez que el desarrollo de un proyecto alcance una "milestone" (hito) propuesta o cierre de ciclo de desarrollo, se creará un "tag" de Git con el número de versión (por ejemplo `v1.1.0`) en el repositorio local.
   - Al momento de crear un tag, se debe utilizar el prefijo `v` para indicar que se trata de un número de versión, por ejemplo: `v1.0.0`, `v2.3.1`, etc.
   - Una vez mergeada la rama de desarrollo a la rama principal (main), se deberá crear el tag correspondiente en el repositorio local (`git tag v1.0.0`) y luego subirlo al repositorio remoto en GitHub (`git push --tags`).
3. **GitHub Releases:**
   - A partir del tag subido, se deberá crear un *Release* en GitHub.
   - En el Release se detallarán los cambios implementados, aprovechando la visibilidad del historial (que se ve favorecido por Conventional Commits) para comunicar claramente las modificaciones, adiciones o correcciones de la nueva versión.
   - Para esta sección, se puede utilizar la opción de "Generate release notes" que ofrece GitHub, que genera automáticamente un diff de los cambios entre la versión anterior y la nueva, basado en los commits realizados.

### Caso de Uso Interesante
Al usar tags con el esquema de SemVer en los repositorios, es posible instalar librerías o clonar repositorios apuntando exactamente a una versión específica que se sabe es estable, por ejemplo:

```bash
pip install "git+https://github.com/FIUNER-LICA/auth-module.git@v1.1.0[flask]"
```

Esto asegura consistencia absoluta al momento de desplegar aplicaciones, levantar entornos de desarrollo locales o compartir dependencias en el laboratorio.

---

## Consecuencias
- **Positivas**:
  - **Claridad**: Los números de versión tienen significado semántico, facilitando la comprensión del tipo de cambio introducido (funcionalidad o error).
  - **Seguridad en las Dependencias**: Permite integrar librerías propias o de terceros sin temor a roturas sorpresivas de código.
  - **Instalación Específica**: Se pueden instalar o integrar módulos fijando la versión con precisión gracias al uso de tags de git.
  - **Integración Natural**: Combina muy bien con [Conventional Commits (ADR 003)](adr-003-usar-conventional-commits.md), donde un `fix` suele derivar en una versión **PATCH**, `feat` en **MINOR** y los `BREAKING CHANGES` (cambios que rompen la compatibilidad) en **MAJOR**.
- **Negativas**:
  - Requiere disciplina por parte de los desarrolladores para no olvidar taggear los repositorios, y para entender cuándo un cambio amerita un salto en MAJOR, MINOR o PATCH.
  - Implica un ligero esfuerzo adicional al generar los Releases y la documentación correspondiente en GitHub para cada hito.

## Alternativas Consideradas
- **Versionado basado en fechas (Calendar Versioning o CalVer)**: Útil en sistemas donde el paso del tiempo es el principal indicador, pero no comunica información sobre la compatibilidad de las APIs o librerías que interconectamos en nuestros proyectos. [Referencia](https://calver.org/)
- **Versionado incremental simple (v1, v2, v3)**: Es más sencillo pero pierde toda la expresividad y control en pequeños cambios o corrección de errores.

## Fecha
05/10/2026

## Autor
- [Caupolicán Ré](https://github.com/caupolicanre)

## Referencias
- [Sitio principal de Semantic Versioning](https://semver.org/)
- [Especificación Semantic Versioning 2.0.0](https://semver.org/spec/v2.0.0.html)
- [ADR 003: Uso de Conventional Commits](/docs/adr-003-usar-conventional-commits.md)
- [A successful Git branching model](https://nvie.com/posts/a-successful-git-branching-model/) (Driessen method)
