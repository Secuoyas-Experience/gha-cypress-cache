# gha-cypress-cache

Esta accion permite generar la cache de los `node_modules` y de la cache de Cypress para un proyecto de Cypress.

## Ejemplo

En el siguiente ejemplo se muestra como utilizar el action `gha-cypress-cache` antes de cualquier trabajo de cypress que use esa cache.

```yaml
name: cypress-griddo

on:
  workflow_dispatch:

jobs:
  cypress-cache:
    runs-on: toolbox-griddo-qa
    steps:
      - uses: Secuoyas-Experience/gha-cypress-cache@v1

  cypress-tests:
    runs-on: toolbox-griddo-qa
    needs:
        - cypress-cache
    steps:
        ...
```

Por defecto los directorios donde se encuentran los ficheros cacheados son:

- `node_modules`: todas las dependencias del proyecto
- `.cache`: dependencias en general
- `.cache/Cypress`: dependencias de Cypress