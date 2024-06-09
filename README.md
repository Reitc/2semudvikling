# 2semudvikling

# Eksempel 1

# Vue Project for Eksamensopgaver

## Indhold
1. [Projektbeskrivelse](#projektbeskrivelse)
2. [Installation og Opsætning](#installation-og-opsætning)
3. [GitHub Flow](#github-flow)
4. [Statisk Kodeanalyse](#statisk-kodeanalyse)
5. [Refaktoreringsdokumentation](#refaktoreringsdokumentation)
6. [Unit Testing](#unit-testing)
7. [End-To-End (E2E) Testing](#end-to-end-e2e-testing)
8. [Konklusion](#konklusion)

## Projektbeskrivelse
Dette projekt er en del af eksamensopgaverne og er et Vue.js projekt, der anvender Git til versionsstyring. Projektet inkluderer statisk kodeanalyse, refaktorisering, unit tests og End-To-End (E2E) tests. Projektet er hostet på GitHub og følger et GitHub flow til CI/CD.

## Installation og Opsætning
Følg disse trin for at klone og opsætte projektet lokalt:

1. Klon repository:
    ```sh
    git clone https://github.com/din-bruger/vue-eksamensprojekt.git
    ```
2. Naviger til projektmappen:
    ```sh
    cd vue-eksamensprojekt
    ```
3. Installer afhængigheder:
    ```sh
    npm install
    ```
4. Start udviklingsserveren:
    ```sh
    npm run dev
    ```

## GitHub Flow
Dette projekt anvender GitHub Actions til CI/CD. Følgende workflow konfigureres til at køre ved hvert push:

```yaml
name: 'Linting and testing'

on: push

jobs:
  linting:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: install packages
        run: npm install
      - name: run lint
        run: npm run lint

  E2ETest:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
        with:
          install: npm install
      - name: Cypress run
        uses: cypress-io/github-action@v6
        with:
          start: npm run dev

  UnitTest:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: install packages
        run: npm install
      - name: Run unit tests
        run: npm run test:unit
