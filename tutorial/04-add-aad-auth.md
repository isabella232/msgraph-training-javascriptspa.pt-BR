---
ms.openlocfilehash: 77f74be505d72c6c0fd55d5f2650e32d03d63348
ms.sourcegitcommit: 18785a430bc1885ccac1ebbe1f3eba634c58bea8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/30/2020
ms.locfileid: "48822761"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="2ad59-101">Neste exercício, você estenderá o aplicativo do exercício anterior para oferecer suporte à autenticação com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2ad59-101">In this exercise you will extend the application from the previous exercise to support authentication with Azure AD.</span></span> <span data-ttu-id="2ad59-102">Isso é necessário para obter o token de acesso OAuth necessário para chamar o Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="2ad59-102">This is required to obtain the necessary OAuth access token to call the Microsoft Graph.</span></span> <span data-ttu-id="2ad59-103">Nesta etapa, você integrará a biblioteca da [biblioteca de autenticação da Microsoft](https://github.com/AzureAD/microsoft-authentication-library-for-js) ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2ad59-103">In this step you will integrate the [Microsoft Authentication Library](https://github.com/AzureAD/microsoft-authentication-library-for-js) library into the application.</span></span>

1. <span data-ttu-id="2ad59-104">Crie um novo arquivo no diretório raiz chamado **config.js** e adicione o código a seguir.</span><span class="sxs-lookup"><span data-stu-id="2ad59-104">Create a new file in the root directory named **config.js** and add the following code.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/config.example.js" id="msalConfigSnippet":::

    <span data-ttu-id="2ad59-105">Substitua `YOUR_APP_ID_HERE` pela ID do aplicativo do portal de registro do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2ad59-105">Replace `YOUR_APP_ID_HERE` with the application ID from the Application Registration Portal.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="2ad59-106">Se você estiver usando o controle de origem como o Git, agora seria uma boa hora para excluir o arquivo **config.js** do controle de origem para evitar vazar inadvertidamente sua ID de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2ad59-106">If you're using source control such as git, now would be a good time to exclude the **config.js** file from source control to avoid inadvertently leaking your app ID.</span></span>

1. <span data-ttu-id="2ad59-107">Abra **auth.js** e adicione o seguinte código ao início do arquivo.</span><span class="sxs-lookup"><span data-stu-id="2ad59-107">Open **auth.js** and add the following code to the beginning of the file.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/auth.js" id="authInitSnippet":::

## <a name="implement-sign-in"></a><span data-ttu-id="2ad59-108">Implementar logon</span><span class="sxs-lookup"><span data-stu-id="2ad59-108">Implement sign-in</span></span>

<span data-ttu-id="2ad59-109">Nesta seção, você implementará as `signIn` `signOut` funções e.</span><span class="sxs-lookup"><span data-stu-id="2ad59-109">In this section you'll implement the `signIn` and `signOut` functions.</span></span>

1. <span data-ttu-id="2ad59-110">Substitua a função `signIn` existente pelo seguinte.</span><span class="sxs-lookup"><span data-stu-id="2ad59-110">Replace the existing `signIn` function with the following.</span></span>

    ```javascript
    async function signIn() {
      // Login
      try {
        // Use MSAL to login
        const authResult = await msalClient.loginPopup(msalRequest);
        console.log('id_token acquired at: ' + new Date().toString());
        // Save the account username, needed for token acquisition
        sessionStorage.setItem('msalAccount', authResult.account.username);
        // TEMPORARY
        updatePage(Views.error, {
          message: 'Login successful',
          debug: `Token: ${authResult.accessToken}`
        });
      } catch (error) {
        console.log(error);
        updatePage(Views.error, {
          message: 'Error logging in',
          debug: error
        });
      }
    }
    ```

    <span data-ttu-id="2ad59-111">Este código temporário exibirá o token de acesso após um logon bem-sucedido.</span><span class="sxs-lookup"><span data-stu-id="2ad59-111">This temporary code will display the access token after a successful login.</span></span>

1. <span data-ttu-id="2ad59-112">Substitua a função `signOut` existente pelo seguinte.</span><span class="sxs-lookup"><span data-stu-id="2ad59-112">Replace the existing `signOut` function with the following.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/auth.js" id="signOutSnippet":::

1. <span data-ttu-id="2ad59-113">Salve suas alterações e atualize a página.</span><span class="sxs-lookup"><span data-stu-id="2ad59-113">Save your changes and refresh the page.</span></span> <span data-ttu-id="2ad59-114">Depois de entrar, você verá uma caixa de erro que mostra o token de acesso.</span><span class="sxs-lookup"><span data-stu-id="2ad59-114">After you sign in, you should see an error box that shows the access token.</span></span>

## <a name="get-the-users-profile"></a><span data-ttu-id="2ad59-115">Obter o perfil do usuário</span><span class="sxs-lookup"><span data-stu-id="2ad59-115">Get the user's profile</span></span>

<span data-ttu-id="2ad59-116">Nesta seção, você melhorará a `signIn` função de usar o token de acesso para obter o perfil do usuário do Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="2ad59-116">In this section you'll improve the `signIn` function to use the access token to get the user's profile from Microsoft Graph.</span></span>

1. <span data-ttu-id="2ad59-117">Adicione a seguinte função no **auth.js** para recuperar o token de acesso do usuário.</span><span class="sxs-lookup"><span data-stu-id="2ad59-117">Add the following function in **auth.js** to retrieve the user's access token.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/auth.js" id="getTokenSnippet":::

1. <span data-ttu-id="2ad59-118">Crie um novo arquivo na raiz do projeto chamado **graph.js** e adicione o código a seguir.</span><span class="sxs-lookup"><span data-stu-id="2ad59-118">Create a new file in the root of the project named **graph.js** and add the following code.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/graph.js" id="graphInitSnippet":::

    <span data-ttu-id="2ad59-119">Este código cria um provedor de autorização que envolve o `getToken` método em **auth.js** e inicializa o cliente de gráfico com esse provedor.</span><span class="sxs-lookup"><span data-stu-id="2ad59-119">This code creates an authorization provider that wraps the `getToken` method in **auth.js** , and initializes the Graph client with this provider.</span></span>

1. <span data-ttu-id="2ad59-120">Adicione a seguinte função no **graph.js** para obter o perfil do usuário.</span><span class="sxs-lookup"><span data-stu-id="2ad59-120">Add the following function in **graph.js** to get the user's profile.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/graph.js" id="getUserSnippet":::

1. <span data-ttu-id="2ad59-121">Substitua a função `signIn` existente pelo seguinte.</span><span class="sxs-lookup"><span data-stu-id="2ad59-121">Replace the existing `signIn` function with the following.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/auth.js" id="signInSnippet":::

1. <span data-ttu-id="2ad59-122">Salve suas alterações e atualize a página.</span><span class="sxs-lookup"><span data-stu-id="2ad59-122">Save your changes and refresh the page.</span></span> <span data-ttu-id="2ad59-123">Depois de entrar, você deve terminar de volta na Home Page, mas a interface do usuário deve ser alterada para indicar que você está conectado.</span><span class="sxs-lookup"><span data-stu-id="2ad59-123">After you sign in, you should end up back on the home page, but the UI should change to indicate that you are signed-in.</span></span>

    ![Uma captura de tela da Home Page após entrar](./images/user-signed-in.png)

1. <span data-ttu-id="2ad59-125">Clique no avatar do usuário no canto superior direito para **acessar o link sair.**</span><span class="sxs-lookup"><span data-stu-id="2ad59-125">Click the user avatar in the top right corner to access the **Sign out** link.</span></span> <span data-ttu-id="2ad59-126">Clicar **em sair** redefine a sessão e retorna à Home Page.</span><span class="sxs-lookup"><span data-stu-id="2ad59-126">Clicking **Sign out** resets the session and returns you to the home page.</span></span>

    ![Uma captura de tela do menu suspenso com o link sair](./images/sign-out-button.png)

## <a name="storing-and-refreshing-tokens"></a><span data-ttu-id="2ad59-128">Armazenar e atualizar tokens</span><span class="sxs-lookup"><span data-stu-id="2ad59-128">Storing and refreshing tokens</span></span>

<span data-ttu-id="2ad59-129">Nesse ponto, seu aplicativo tem um token de acesso, que é enviado no `Authorization` cabeçalho das chamadas de API.</span><span class="sxs-lookup"><span data-stu-id="2ad59-129">At this point your application has an access token, which is sent in the `Authorization` header of API calls.</span></span> <span data-ttu-id="2ad59-130">Este é o token que permite que o aplicativo acesse o Microsoft Graph em nome do usuário.</span><span class="sxs-lookup"><span data-stu-id="2ad59-130">This is the token that allows the app to access the Microsoft Graph on the user's behalf.</span></span>

<span data-ttu-id="2ad59-131">No entanto, esse token é de vida curta.</span><span class="sxs-lookup"><span data-stu-id="2ad59-131">However, this token is short-lived.</span></span> <span data-ttu-id="2ad59-132">O token expira uma hora após sua emissão.</span><span class="sxs-lookup"><span data-stu-id="2ad59-132">The token expires an hour after it is issued.</span></span> <span data-ttu-id="2ad59-133">É onde o token de atualização se torna útil.</span><span class="sxs-lookup"><span data-stu-id="2ad59-133">This is where the refresh token becomes useful.</span></span> <span data-ttu-id="2ad59-134">O token de atualização permite que o aplicativo solicite um novo token de acesso sem exigir que o usuário entre novamente.</span><span class="sxs-lookup"><span data-stu-id="2ad59-134">The refresh token allows the app to request a new access token without requiring the user to sign in again.</span></span>

<span data-ttu-id="2ad59-135">Como o aplicativo está usando a biblioteca MSAL, você não precisa implementar qualquer lógica de armazenamento ou de atualização.</span><span class="sxs-lookup"><span data-stu-id="2ad59-135">Because the app is using the MSAL library, you do not have to implement any token storage or refresh logic.</span></span> <span data-ttu-id="2ad59-136">O MSAL armazena em cache o token na sessão do navegador.</span><span class="sxs-lookup"><span data-stu-id="2ad59-136">MSAL caches the token in the browser session.</span></span> <span data-ttu-id="2ad59-137">O `acquireTokenSilent` método primeiro verifica o token em cache e, se ele não tiver expirado, ele o retornará.</span><span class="sxs-lookup"><span data-stu-id="2ad59-137">The `acquireTokenSilent` method first checks the cached token, and if it is not expired, it returns it.</span></span> <span data-ttu-id="2ad59-138">Se ele tiver expirado, ele usará o token de atualização em cache para obter um novo.</span><span class="sxs-lookup"><span data-stu-id="2ad59-138">If it is expired, it uses the cached refresh token to obtain a new one.</span></span> <span data-ttu-id="2ad59-139">O objeto de cliente Graph chama o `getToken` método em **auth.js** em todas as solicitações, garantindo que ele tenha um token atualizado.</span><span class="sxs-lookup"><span data-stu-id="2ad59-139">The Graph client object calls the `getToken` method in **auth.js** on every request, ensuring that it has an up-to-date token.</span></span>
