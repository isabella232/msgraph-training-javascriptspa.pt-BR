---
ms.openlocfilehash: 177f436812050ab4e9bf6c86bb5229b30f0f885b
ms.sourcegitcommit: 18785a430bc1885ccac1ebbe1f3eba634c58bea8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/30/2020
ms.locfileid: "48822778"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="9b42c-101">Nesta seção, você adicionará a capacidade de criar eventos no calendário do usuário.</span><span class="sxs-lookup"><span data-stu-id="9b42c-101">In this section you will add the ability to create events on the user's calendar.</span></span>

## <a name="create-a-new-event-form"></a><span data-ttu-id="9b42c-102">Criar um novo formulário de eventos</span><span class="sxs-lookup"><span data-stu-id="9b42c-102">Create a new event form</span></span>

1. <span data-ttu-id="9b42c-103">Adicione a seguinte função a **ui.js** para renderizar um formulário para o novo evento.</span><span class="sxs-lookup"><span data-stu-id="9b42c-103">Add the following function to **ui.js** to render a form for the new event.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/ui.js" id="showNewEventFormSnippet":::

## <a name="create-the-event"></a><span data-ttu-id="9b42c-104">Criar o evento</span><span class="sxs-lookup"><span data-stu-id="9b42c-104">Create the event</span></span>

1. <span data-ttu-id="9b42c-105">Adicione a seguinte função a **graph.js** para ler os valores do formulário e criar um novo evento.</span><span class="sxs-lookup"><span data-stu-id="9b42c-105">Add the following function to **graph.js** to read the values from the form and create a new event.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/graph.js" id="createEventSnippet":::

1. <span data-ttu-id="9b42c-106">Salve suas alterações e atualize o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9b42c-106">Save your changes and refresh the app.</span></span> <span data-ttu-id="9b42c-107">Clique no item de navegação **calendário** e, em seguida, clique no botão **criar evento** .</span><span class="sxs-lookup"><span data-stu-id="9b42c-107">Click the **Calendar** nav item, then click the **Create event** button.</span></span> <span data-ttu-id="9b42c-108">Preencha os valores e clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="9b42c-108">Fill in the values and click **Create**.</span></span> <span data-ttu-id="9b42c-109">O aplicativo retorna para o modo de exibição calendário depois que o novo evento é criado.</span><span class="sxs-lookup"><span data-stu-id="9b42c-109">The app returns to the calendar view once the new event is created.</span></span>

    ![Uma captura de tela do novo formulário de evento](images/create-event-01.png)
