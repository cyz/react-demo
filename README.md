# 🎭 Playwright: Rick And Morty API com React

Repositório com exemplo de implementação do **[Playwright](https://playwright.dev/)**, um framework open source de testes E2E da Microsoft. Este app foi criado com o template [Create React App](https://github.com/facebook/create-react-app) e consome dados da [Rick and Morty API](https://rickandmortyapi.com/).

## 🔥 Executando as Demos!

Basta seguir os comando abaixo:

```bash
> git clone https://github.com/cyz/react-demo.git
> cd react-demo
> # instalando das dependências
> yarn install 
> # inicializando a aplicação localmente
> yarn start
```

### Instalação do Yarn:
Se você não tem o yarn instalado, execute o comando:
```bash
> npm install --g yarn
```

## Cobertura de Testes com Playwright
Para configurar os testes, vamos utilizar o Playwright CLI. No terminal do seu VSCode, execute os seguintes comandos:

```bash
> yarn create playwright --ct
```

O `--ct` no comando acima direcionará a Playwright CLI para configurar testas de componentes. Durante o processo de configuração, selecione `JavaScript` como a linguagem de programação para escrever os testes E2E e `React` como a opção de framework. Ao final da execução, o Playwright estará instalado em seu app.

Todas as configurações geradas pelo Playwright serão armazenadas em um arquivo chamado `playwright-ct.config.js`, que será criado na pasta raiz do seu projeto. Você pode ajustar as configurações padrão deste arquivo sempre que for necessário.

### Adicionando testes
Clique no `Explorer` do menu lateral do VSCode para visualizar o conteúdo do seu projeto. Dentro da pasta `src` e crie uma pasta chamada `tests`. Essa pasta, irá receber todos os arquivos de testes que serão lidos pelo Playwright.

Na pasta `tests`, você deverá criar um arquivo chamado `SearchField.spec.jsx`. Este arquivo terá os casos de teste para o componente SearchField. O Playwright reconhece que arquivos com a extensão `.spec` são utilizados para testes.

Copie o script abaixo para seu arquivo `SearchField.spec.jsx` e salve:

```javascript
import { test, expect } from '@playwright/experimental-ct-react';
import App, { SearchField } from '../App';

test('SearchField accepts text input', async ({ mount }) => {
    const searchComponent = await mount(
        <SearchField />
    );
    const searchField = searchComponent.locator('#search-field')
    
    await searchField.fill('Rick')
    await expect(searchField).toHaveValue('Rick')
    
});

test('Clicking `Find Character` button executes executeSearch prop', async ({ mount }) => {
    let isCalled = false

    const searchComponent = await mount(
        <SearchField
            executeSearch={() => isCalled = true}
        />
    );

    await searchComponent.locator('#search-field').fill('test character')
    await searchComponent.locator('#find').click()
    

    expect(isCalled).toBeTruthy()
});

test('Input field text length controls `Find Character` button disabled state', async ({ mount }) => {
    const searchComponent = await mount(
        <SearchField />
    );

    const btn = await searchComponent.locator('#find').isDisabled()
    expect(btn).toBeTruthy()

    await searchComponent.locator('#search-field').fill('test character')
    await expect(searchComponent.locator('#find')).toBeEnabled();
});
```

Feito isso, é hora de executar o teste!

```bash
> yarn test-ct
```

Por padrão, os testes de componentes serão executados sem abrir os navegadores Chromium, Webkit e Firefox. O Playwright possui um recurso integrado para gerar um relatório HTML para cada execução de teste. O relatório HTML contém o nome do teste, o status da execução e a duração de cada caso de teste.

Acesse o relatório usando o comando:
```bash
> npx playwright show-report
```

Se você quiser ver cada teste em execução ou até mesmo definir que cada execução gere um screenshot de tela, acesse o arquivo `playwright-ct.config.js` e inclua as seguintes instruções no trecho `use`:

```javascript
  use: {
    /* Collect trace when retrying the failed test. See https://playwright.dev/docs/trace-viewer */
    trace: 'on-first-retry',

    /* Capture component screenshot */
    screenshot: "on",

    /* Define browser opening for each test. 
    By default, the headless is true and execute test without opening the Chromium, Webkit, and Firefox browsers */
    headless: false,

    /* Port to use for Playwright component endpoint. */
    ctPort: 3100,
  }
```

## 🚀 Recursos Utilizados

* **[Playwright](https://www.npmjs.com/package/playwright)**
* **[Vs Code Extensions - Playwright Snippets](https://marketplace.visualstudio.com/items?itemName=nitayneeman.playwright-snippets&wt.mc_id=seriespg_17010_webpage_reactor)**
* **[TypeScript](https://www.typescriptlang.org/download)**
* **[Visual Studio Code](https://code.visualstudio.com/?wt.mc_id=seriespg_17010_webpage_reactor)**
* **[Node.js](https://nodejs.org/en/)**
* **[ts-node](https://www.npmjs.com/package/ts-node)**

## :link: Links & Recursos Importantes

- ✅ **[Documentação Oficial do Playwright](https://playwright.dev/docs/intro)**
- ✅ **[Documentação Oficial do TypeScript](http://typescriptlang.org/docs/handbook/)**
- ✅ **[TypeScript no Visual Studio Code](https://code.visualstudio.com/docs/languages/typescript?wt.mc_id=seriespg_17010_webpage_reactor)**
- ✅ **[Compilando Códigos TypeScript no Vs Code](https://code.visualstudio.com/docs/typescript/typescript-compiling?wt.mc_id=seriespg_17010_webpage_reactor)**
- ✅ **[Tutorial TypeScript no Vs Code](https://code.visualstudio.com/docs/typescript/typescript-tutorial?wt.mc_id=seriespg_17010_webpage_reactor)**
- ✅ **[Curso Grátis de Node.js](https://docs.microsoft.com/learn/paths/build-javascript-applications-nodejs/?wt.mc_id=seriespg_17010_webpage_reactor)**
- ✅ **[Curso Grátis de TypeScript](https://docs.microsoft.com/learn/paths/build-javascript-applications-typescript/?wt.mc_id=seriespg_17010_webpage_reactor)**

## :sos: Dúvidas

Caso tenham dúvidas, sintam-se à vontade em abrir uma **[ISSUE AQUI](https://github.com/cyz/react-demo/issues)**.
