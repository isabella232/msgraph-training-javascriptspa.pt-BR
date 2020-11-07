---
ms.openlocfilehash: 1f2ff0e013bd1b104cd5b353ba2da542382657ab
ms.sourcegitcommit: 18785a430bc1885ccac1ebbe1f3eba634c58bea8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/30/2020
ms.locfileid: "48822775"
---
<!-- markdownlint-disable MD002 MD041 -->

Neste exercício, você incorporará o Microsoft Graph no aplicativo. Para este aplicativo, você usará a biblioteca de [biblioteca de cliente JavaScript do Microsoft Graph](https://github.com/microsoftgraph/msgraph-sdk-javascript) para fazer chamadas para o Microsoft Graph.

## <a name="get-calendar-events-from-outlook"></a>Obter eventos de calendário do Outlook

Nesta seção, você usará a biblioteca de cliente do Microsoft Graph para obter eventos de calendário do usuário.

1. Crie um novo arquivo na raiz do projeto chamado **timezones.js** e adicione o código a seguir.

    :::code language="javascript" source="../demo/graph-tutorial/timezones.js" id="zoneMappingsSnippet":::

    Este código mapeia os identificadores de fuso horário do Windows para os identificadores de fuso horário da IANA para compatibilidade com o moment.js.

1. Adicione a função a seguir para **graph.js**.

    :::code language="javascript" source="../demo/graph-tutorial/graph.js" id="getEventsSnippet":::

    Considere o que esse código está fazendo.

    - A URL que será chamada é `/me/calendarview` .
    - O `header` método adiciona um `Prefer` cabeçalho especificando o fuso horário preferencial do usuário.
    - O `query` método adiciona as horas de início e de término para o modo de exibição de calendário.
    - O `select` método limita os campos retornados para cada evento para apenas aqueles que o modo de exibição realmente usará.
    - O `orderby` método classifica os resultados pela hora de início, com o evento mais antigo sendo o primeiro.
    - O `top` método solicita até 50 eventos na resposta.

1. Abra **ui.js** e adicione a função a seguir.

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

1. Atualize a `switch` instrução na `updatePage` função para chamar `showCalendar` quando o modo de exibição é `Views.calendar` .

    :::code language="javascript" source="../demo/graph-tutorial/ui.js" id="updatePageSnippet" highlight="18-20":::

1. Salve suas alterações e atualize o aplicativo. Entre e clique no link **calendário** na barra de navegação. Se tudo funcionar, você deverá ver um despejo JSON de eventos no calendário do usuário.

## <a name="display-the-results"></a>Exibir os resultados

Nesta seção, você atualizará a `showCalendar` função para exibir os eventos de forma mais amigável.

1. Substitua a função `showCalendar` existente pelo seguinte.

    :::code language="javascript" source="../demo/graph-tutorial/ui.js" id="showCalendarSnippet":::

    Isso faz um loop pela coleção de eventos e adiciona uma linha de tabela para cada um.

1. Salve as alterações e atualize o aplicativo. Clique no link do **calendário** e o aplicativo agora deve renderizar uma tabela de eventos para a semana atual.

    ![Uma captura de tela da tabela de eventos](./images/calendar-list.png)
