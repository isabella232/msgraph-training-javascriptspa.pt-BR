---
ms.openlocfilehash: 177f436812050ab4e9bf6c86bb5229b30f0f885b
ms.sourcegitcommit: 18785a430bc1885ccac1ebbe1f3eba634c58bea8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/30/2020
ms.locfileid: "48822778"
---
<!-- markdownlint-disable MD002 MD041 -->

Nesta seção, você adicionará a capacidade de criar eventos no calendário do usuário.

## <a name="create-a-new-event-form"></a>Criar um novo formulário de eventos

1. Adicione a seguinte função a **ui.js** para renderizar um formulário para o novo evento.

    :::code language="javascript" source="../demo/graph-tutorial/ui.js" id="showNewEventFormSnippet":::

## <a name="create-the-event"></a>Criar o evento

1. Adicione a seguinte função a **graph.js** para ler os valores do formulário e criar um novo evento.

    :::code language="javascript" source="../demo/graph-tutorial/graph.js" id="createEventSnippet":::

1. Salve suas alterações e atualize o aplicativo. Clique no item de navegação **calendário** e, em seguida, clique no botão **criar evento** . Preencha os valores e clique em **criar**. O aplicativo retorna para o modo de exibição calendário depois que o novo evento é criado.

    ![Uma captura de tela do novo formulário de evento](images/create-event-01.png)
