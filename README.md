# 2semudvikling

# Eksempel 1

# Vue Project for Eksamensopgaver

## Indhold
1. Projektbeskrivelse
2. Installation og Opsætning
3. GitHub Flow
4. Statisk Kodeanalyse
5. Refaktoreringsdokumentation
6. Unit Testing
7. End-To-End (E2E) Testing
8. Konklusion

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
```
## Refaktorisering med Statisk Kodeanalyse
### ESLint
Projektet bruger ESLint til statisk kodeanalyse for at sikre, at koden opfylder god praksis og standarder. Følg disse trin for at køre ESLint:

1. Kør linting:
    ```sh
    npm run lint
    ```

### Refaktorering
Under refaktoreringen blev følgende ændringer foretaget for at opfylde ESLint regler og god praksis:
- Unødvendige variabler blev fjernet.
- Koden blev omstruktureret for bedre læsbarhed.
- Brug af `const` og `let` i stedet for `var`.
- Ensartede anførselstegn blev anvendt.

## Unit Testing
Projektet bruger Jest til unit tests. Der er skrevet mindst 5 unit tests for forskellige komponenter. Følg disse trin for at køre unit tests:

1. Kør unit tests:
    ```sh
    npm run test:unit
    ```

### Eksempel på Unit Test
```javascript
import { shallowMount } from '@vue/test-utils'
import Counter from '@/components/Counter.vue'

describe('Counter.vue', () => {
  it('renders initial count', () => {
    const wrapper = shallowMount(Counter)
    expect(wrapper.text()).toContain('0')
  })

  it('increments count when increment button is clicked', async () => {
    const wrapper = shallowMount(Counter)
    const incrementButton = wrapper.find('button')
    await incrementButton.trigger('click')
    expect(wrapper.text()).toContain('1')
  })

  it('decrements count when decrement button is clicked', async () => {
    const wrapper = shallowMount(Counter)
    const decrementButton = wrapper.findAll('button').at(1)
    await decrementButton.trigger('click')
    expect(wrapper.text()).toContain('-1')
  })
})
```
## End-to-End (E2E) Testing
Projektet bruger Cypress til E2E tests. To vigtige scenarier er blevet testet for at sikre, at applikationen fungerer som forventet. Følg disse trin for at køre E2E tests:

1. Kør E2E tests:
    ```sh
    npm run test:e2e
    ```

### Eksempel på E2E Test
```javascript
describe('To-Do List', () => {
  it('displays the to-do list', () => {
    cy.visit('/')
    cy.contains('h1', 'To-Do List')
    cy.get('ul').children().should('have.length', 2)
    cy.get('ul').children().first().should('contain', 'Task 1')
    cy.get('ul').children().last().should('contain', 'Task 2')
  })
})
```
## GitHub Flow
Dette projekt følger GitHub flow for kontinuerlig integration og levering (CI/CD). Når ændringer bliver committet til repositoryet, udføres følgende handlinger automatisk ved hjælp af GitHub Actions:

### Workflow Fil
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
```
