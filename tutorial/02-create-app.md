---
ms.openlocfilehash: 0ef683278142776d6895b8655dd16e3635b90fa4
ms.sourcegitcommit: 18785a430bc1885ccac1ebbe1f3eba634c58bea8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/30/2020
ms.locfileid: "48822774"
---
<!-- markdownlint-disable MD002 MD041 -->

Comece criando um diretório vazio para o projeto. Isso pode ser em um servidor HTTP ou em um diretório em sua máquina de desenvolvimento. Se ele estiver em sua máquina de desenvolvimento, você precisará copiá-lo para um servidor para teste ou executar um servidor HTTP em sua máquina de desenvolvimento. Se você não tiver um desses, a próxima seção fornecerá instruções.

## <a name="start-a-local-web-server-optional"></a>Iniciar um servidor Web local (opcional)

> [!NOTE]
> As etapas desta seção exigem [Node.js](https://nodejs.org).

Nesta seção, você usará [http-Server](https://www.npmjs.com/package/http-server) para executar um servidor http simples a partir da linha de comando.

1. Abra a interface de linha de comando (CLI) no diretório que você criou para o projeto.
1. Execute o seguinte comando para iniciar um servidor Web nesse diretório.

    ```Shell
    npx http-server -c-1
    ```

1. Abra o navegador e navegue até `http://localhost:8080` .

Você verá um **índice de/** página. Isso confirma que o servidor HTTP está em execução.

![Uma captura de tela da página de índice servida por http-Server.](images/run-web-server.png)

## <a name="design-the-app"></a>Projetar o aplicativo

Nesta seção, você criará o layout básico de interface do usuário para o aplicativo.

1. Crie um novo arquivo na raiz do projeto chamado **index.html** e adicione o código a seguir.

    :::code language="html" source="../demo/graph-tutorial/index.html" id="indexSnippet":::

    Isso define o layout básico do aplicativo, incluindo uma barra de navegação. Ele também adiciona o seguinte:

    - [Bootstrap](https://getbootstrap.com/) e seu JavaScript de suporte
    - [FontAwesome](https://fontawesome.com/)
    - [Moment.js](https://momentjs.com/)
    - [Biblioteca de autenticação da Microsoft para JavaScript (MSAL.js) 2,0](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-browser)
    - [Biblioteca de cliente JavaScript do Microsoft Graph](https://github.com/microsoftgraph/msgraph-sdk-javascript)

    > [!TIP]
    > A página inclui um favicon ( `<link rel="shortcut icon" href="g-raph.png">` ). Você pode remover essa linha ou pode baixar o arquivo de **g-raph.png** do [GitHub](https://github.com/microsoftgraph/g-raph).

1. Crie um novo arquivo chamado **Style. css** e adicione o código a seguir.

    :::code language="css" source="../demo/graph-tutorial/style.css":::

1. Crie um novo arquivo chamado **auth.js** e adicione o código a seguir.

    ```javascript
    function signIn() {
      // TEMPORARY
      updatePage({name: 'Megan Bowen', userName: 'meganb@contoso.com'});
    }

    function signOut() {
      // TEMPORARY
      updatePage();
    }
    ```

1. Crie um novo arquivo chamado **ui.js** e adicione o código a seguir.

    ```javascript
    // Select DOM elements to work with
    const authenticatedNav = document.getElementById('authenticated-nav');
    const accountNav = document.getElementById('account-nav');
    const mainContainer = document.getElementById('main-container');

    const Views = { error: 1, home: 2, calendar: 3 };

    function createElement(type, className, text) {
      var element = document.createElement(type);
      element.className = className;

      if (text) {
        var textNode = document.createTextNode(text);
        element.appendChild(textNode);
      }

      return element;
    }

    function showAuthenticatedNav(user, view) {
      authenticatedNav.innerHTML = '';

      if (user) {
        // Add Calendar link
        var calendarNav = createElement('li', 'nav-item');

        var calendarLink = createElement('button',
          `btn btn-link nav-link${view === Views.calendar ? ' active' : '' }`,
          'Calendar');
        calendarLink.setAttribute('onclick', 'getEvents();');
        calendarNav.appendChild(calendarLink);

        authenticatedNav.appendChild(calendarNav);
      }
    }

    function showAccountNav(user) {
      accountNav.innerHTML = '';

      if (user) {
        // Show the "signed-in" nav
        accountNav.className = 'nav-item dropdown';

        var dropdown = createElement('a', 'nav-link dropdown-toggle');
        dropdown.setAttribute('data-toggle', 'dropdown');
        dropdown.setAttribute('role', 'button');
        accountNav.appendChild(dropdown);

        var userIcon = createElement('i',
          'far fa-user-circle fa-lg rounded-circle align-self-center');
        userIcon.style.width = '32px';
        dropdown.appendChild(userIcon);

        var menu = createElement('div', 'dropdown-menu dropdown-menu-right');
        dropdown.appendChild(menu);

        var userName = createElement('h5', 'dropdown-item-text mb-0', user.displayName);
        menu.appendChild(userName);

        var userEmail = createElement('p', 'dropdown-item-text text-muted mb-0', user.mail || user.userPrincipalName);
        menu.appendChild(userEmail);

        var divider = createElement('div', 'dropdown-divider');
        menu.appendChild(divider);

        var signOutButton = createElement('button', 'dropdown-item', 'Sign out');
        signOutButton.setAttribute('onclick', 'signOut();');
        menu.appendChild(signOutButton);
      } else {
        // Show a "sign in" button
        accountNav.className = 'nav-item';

        var signInButton = createElement('button', 'btn btn-link nav-link', 'Sign in');
        signInButton.setAttribute('onclick', 'signIn();');
        accountNav.appendChild(signInButton);
      }
    }

    function showWelcomeMessage(user) {
      // Create jumbotron
      var jumbotron = createElement('div', 'jumbotron');

      var heading = createElement('h1', null, 'JavaScript SPA Graph Tutorial');
      jumbotron.appendChild(heading);

      var lead = createElement('p', 'lead',
        'This sample app shows how to use the Microsoft Graph API to access' +
        ' a user\'s data from JavaScript.');
      jumbotron.appendChild(lead);

      if (user) {
        // Welcome the user by name
        var welcomeMessage = createElement('h4', null, `Welcome ${user.displayName}!`);
        jumbotron.appendChild(welcomeMessage);

        var callToAction = createElement('p', null,
          'Use the navigation bar at the top of the page to get started.');
        jumbotron.appendChild(callToAction);
      } else {
        // Show a sign in button in the jumbotron
        var signInButton = createElement('button', 'btn btn-primary btn-large',
          'Click here to sign in');
        signInButton.setAttribute('onclick', 'signIn();')
        jumbotron.appendChild(signInButton);
      }

      mainContainer.innerHTML = '';
      mainContainer.appendChild(jumbotron);
    }

    function showError(error) {
      var alert = createElement('div', 'alert alert-danger');

      var message = createElement('p', 'mb-3', error.message);
      alert.appendChild(message);

      if (error.debug)
      {
        var pre = createElement('pre', 'alert-pre border bg-light p-2');
        alert.appendChild(pre);

        var code = createElement('code', 'text-break text-wrap',
          JSON.stringify(error.debug, null, 2));
        pre.appendChild(code);
      }

      mainContainer.innerHTML = '';
      mainContainer.appendChild(alert);
    }

    function updatePage(view, data) {
      if (!view) {
        view = Views.home;
      }

      const user = JSON.parse(sessionStorage.getItem('graphUser'));

      showAccountNav(user);
      showAuthenticatedNav(user, view);

      switch (view) {
        case Views.error:
          showError(data);
          break;
        case Views.home:
          showWelcomeMessage(user);
          break;
        case Views.calendar:
          break;
      }
    }

    updatePage(Views.home);
    ```

1. Salve todas as suas alterações e atualize a página. Agora, o aplicativo deve ser muito diferente.

    ![Uma captura de tela da página inicial reprojetada](images/app-layout.png)
