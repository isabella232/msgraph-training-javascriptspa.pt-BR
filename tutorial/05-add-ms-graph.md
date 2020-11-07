---
ms.openlocfilehash: 1f2ff0e013bd1b104cd5b353ba2da542382657ab
ms.sourcegitcommit: 18785a430bc1885ccac1ebbe1f3eba634c58bea8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/30/2020
ms.locfileid: "48822775"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="b2a7a-101">Neste exercício, você incorporará o Microsoft Graph no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b2a7a-101">In this exercise you will incorporate the Microsoft Graph into the application.</span></span> <span data-ttu-id="b2a7a-102">Para este aplicativo, você usará a biblioteca de [biblioteca de cliente JavaScript do Microsoft Graph](https://github.com/microsoftgraph/msgraph-sdk-javascript) para fazer chamadas para o Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="b2a7a-102">For this application, you will use the [Microsoft Graph JavaScript Client Library](https://github.com/microsoftgraph/msgraph-sdk-javascript) library to make calls to Microsoft Graph.</span></span>

## <a name="get-calendar-events-from-outlook"></a><span data-ttu-id="b2a7a-103">Obter eventos de calendário do Outlook</span><span class="sxs-lookup"><span data-stu-id="b2a7a-103">Get calendar events from Outlook</span></span>

<span data-ttu-id="b2a7a-104">Nesta seção, você usará a biblioteca de cliente do Microsoft Graph para obter eventos de calendário do usuário.</span><span class="sxs-lookup"><span data-stu-id="b2a7a-104">In this section, you'll use the Microsoft Graph client library to get calendar events for the user.</span></span>

1. <span data-ttu-id="b2a7a-105">Crie um novo arquivo na raiz do projeto chamado **timezones.js** e adicione o código a seguir.</span><span class="sxs-lookup"><span data-stu-id="b2a7a-105">Create a new file in the root of the project named **timezones.js** and add the following code.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/timezones.js" id="zoneMappingsSnippet":::

    <span data-ttu-id="b2a7a-106">Este código mapeia os identificadores de fuso horário do Windows para os identificadores de fuso horário da IANA para compatibilidade com o moment.js.</span><span class="sxs-lookup"><span data-stu-id="b2a7a-106">This code maps Windows time zone identifiers to IANA time zone identifiers for compatibility with moment.js.</span></span>

1. <span data-ttu-id="b2a7a-107">Adicione a função a seguir para **graph.js**.</span><span class="sxs-lookup"><span data-stu-id="b2a7a-107">Add the following function to **graph.js**.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/graph.js" id="getEventsSnippet":::

    <span data-ttu-id="b2a7a-108">Considere o que esse código está fazendo.</span><span class="sxs-lookup"><span data-stu-id="b2a7a-108">Consider what this code is doing.</span></span>

    - <span data-ttu-id="b2a7a-109">A URL que será chamada é `/me/calendarview` .</span><span class="sxs-lookup"><span data-stu-id="b2a7a-109">The URL that will be called is `/me/calendarview`.</span></span>
    - <span data-ttu-id="b2a7a-110">O `header` método adiciona um `Prefer` cabeçalho especificando o fuso horário preferencial do usuário.</span><span class="sxs-lookup"><span data-stu-id="b2a7a-110">The `header` method adds a `Prefer` header specifying the user's preferred time zone.</span></span>
    - <span data-ttu-id="b2a7a-111">O `query` método adiciona as horas de início e de término para o modo de exibição de calendário.</span><span class="sxs-lookup"><span data-stu-id="b2a7a-111">The `query` method adds the start and end times for the calendar view.</span></span>
    - <span data-ttu-id="b2a7a-112">O `select` método limita os campos retornados para cada evento para apenas aqueles que o modo de exibição realmente usará.</span><span class="sxs-lookup"><span data-stu-id="b2a7a-112">The `select` method limits the fields returned for each events to just those the view will actually use.</span></span>
    - <span data-ttu-id="b2a7a-113">O `orderby` método classifica os resultados pela hora de início, com o evento mais antigo sendo o primeiro.</span><span class="sxs-lookup"><span data-stu-id="b2a7a-113">The `orderby` method sorts the results by the start time, with the earliest event being first.</span></span>
    - <span data-ttu-id="b2a7a-114">O `top` método solicita até 50 eventos na resposta.</span><span class="sxs-lookup"><span data-stu-id="b2a7a-114">The `top` method requests up to 50 events in the response.</span></span>

1. <span data-ttu-id="b2a7a-115">Abra **ui.js** e adicione a função a seguir.</span><span class="sxs-lookup"><span data-stu-id="b2a7a-115">Open **ui.js** and add the following function.</span></span>

    ```javascript
    function showCalendar(events) {
      // TEMPORARY
      // Render the results as JSON
      var alert = createElement('div', 'alert alert-success');

      var pre = createElement('pre', 'alert-pre border bg-light p-2');
      alert.appendChild(pre);

      var code = createElement('code', 'text-break',
        JSON.stringify(events, null, 2));
      pre.appendChild(code);

      mainContainer.innerHTML = '';
      mainContainer.appendChild(alert);
    }
    ```

1. <span data-ttu-id="b2a7a-116">Atualize a `switch` instrução na `updatePage` função para chamar `showCalendar` quando o modo de exibição é `Views.calendar` .</span><span class="sxs-lookup"><span data-stu-id="b2a7a-116">Update the `switch` statement in the `updatePage` function to call `showCalendar` when the view is `Views.calendar`.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/ui.js" id="updatePageSnippet" highlight="18-20":::

1. <span data-ttu-id="b2a7a-117">Salve suas alterações e atualize o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b2a7a-117">Save your changes and refresh the app.</span></span> <span data-ttu-id="b2a7a-118">Entre e clique no link **calendário** na barra de navegação.</span><span class="sxs-lookup"><span data-stu-id="b2a7a-118">Sign in and click the **Calendar** link in the nav bar.</span></span> <span data-ttu-id="b2a7a-119">Se tudo funcionar, você deverá ver um despejo JSON de eventos no calendário do usuário.</span><span class="sxs-lookup"><span data-stu-id="b2a7a-119">If everything works, you should see a JSON dump of events on the user's calendar.</span></span>

## <a name="display-the-results"></a><span data-ttu-id="b2a7a-120">Exibir os resultados</span><span class="sxs-lookup"><span data-stu-id="b2a7a-120">Display the results</span></span>

<span data-ttu-id="b2a7a-121">Nesta seção, você atualizará a `showCalendar` função para exibir os eventos de forma mais amigável.</span><span class="sxs-lookup"><span data-stu-id="b2a7a-121">In this section you will update the `showCalendar` function to display the events in a more user-friendly manner.</span></span>

1. <span data-ttu-id="b2a7a-122">Substitua a função `showCalendar` existente pelo seguinte.</span><span class="sxs-lookup"><span data-stu-id="b2a7a-122">Replace the existing `showCalendar` function with the following.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/ui.js" id="showCalendarSnippet":::

    <span data-ttu-id="b2a7a-123">Isso faz um loop pela coleção de eventos e adiciona uma linha de tabela para cada um.</span><span class="sxs-lookup"><span data-stu-id="b2a7a-123">This loops through the collection of events and adds a table row for each one.</span></span>

1. <span data-ttu-id="b2a7a-124">Salve as alterações e atualize o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b2a7a-124">Save the changes and refresh the app.</span></span> <span data-ttu-id="b2a7a-125">Clique no link do **calendário** e o aplicativo agora deve renderizar uma tabela de eventos para a semana atual.</span><span class="sxs-lookup"><span data-stu-id="b2a7a-125">Click on the **Calendar** link and the app should now render a table of events for the current week.</span></span>

    ![Uma captura de tela da tabela de eventos](./images/calendar-list.png)
