# gha-cypress-cache

![GitHub tag (latest by date)](https://img.shields.io/github/v/tag/Secuoyas-Experience/gha-cypress-cache)

Esta acción genera la caché de los `node_modules` y la del binario de Cypress de un proyecto de Cypress, para que los trabajos posteriores ([gha-cypress-run](https://github.com/Secuoyas-Experience/gha-cypress-run) y [gha-cypress-report](https://github.com/Secuoyas-Experience/gha-cypress-report)) la restauren sin volver a instalar nada.

## Requisitos

Desde la `v6` usa `actions/checkout@v7` y `actions/cache@v6`, que se ejecutan con Node.js 24: el runner tiene que ser la versión 2.327.1 o posterior.

## Entradas

- **path**: (opcional) ruta de la caché de Cypress (por defecto `.cache/Cypress`).

## Uso

En el siguiente ejemplo se usa `gha-cypress-cache` antes de cualquier trabajo de Cypress que use esa caché.

```yaml
name: cypress-griddo

on:
  workflow_dispatch:

jobs:
  cypress-cache:
    runs-on: griddo-qa
    steps:
      - uses: Secuoyas-Experience/gha-cypress-cache@v6

  cypress-tests:
    runs-on: griddo-qa
    needs:
      - cypress-cache
    steps:
      ...
```

Las claves de caché incluyen la rama y el hash de `yarn.lock`. Por defecto se cachean:

- `node_modules`: todas las dependencias del proyecto.
- `.cache/Cypress`: el binario de Cypress.
