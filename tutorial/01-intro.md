---
ms.openlocfilehash: bbb1dd429dca4e67735c5fdb2b2280f729115eb2
ms.sourcegitcommit: 18785a430bc1885ccac1ebbe1f3eba634c58bea8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/30/2020
ms.locfileid: "48822757"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="e3e74-101">Este tutorial ensina como criar um aplicativo JavaScript de página única que usa a API do Microsoft Graph para recuperar informações de calendário de um usuário.</span><span class="sxs-lookup"><span data-stu-id="e3e74-101">This tutorial teaches you how to build a JavaScript single-page app that uses the Microsoft Graph API to retrieve calendar information for a user.</span></span>

> [!TIP]
> <span data-ttu-id="e3e74-102">Se preferir baixar o tutorial concluído, você poderá baixar ou clonar o repositório do [GitHub](https://github.com/microsoftgraph/msgraph-training-javascriptspa).</span><span class="sxs-lookup"><span data-stu-id="e3e74-102">If you prefer to just download the completed tutorial, you can download or clone the [GitHub repository](https://github.com/microsoftgraph/msgraph-training-javascriptspa).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e3e74-103">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e3e74-103">Prerequisites</span></span>

<span data-ttu-id="e3e74-104">Antes de iniciar este tutorial, você precisará de acesso a um servidor HTTP para hospedar os arquivos de amostra.</span><span class="sxs-lookup"><span data-stu-id="e3e74-104">Before you start this tutorial, you will need access to an HTTP server to host the sample files.</span></span> <span data-ttu-id="e3e74-105">Pode ser um servidor de teste no seu computador de desenvolvimento ou um servidor remoto.</span><span class="sxs-lookup"><span data-stu-id="e3e74-105">This could be a test server on your development machine, or a remote server.</span></span> <span data-ttu-id="e3e74-106">O tutorial inclui instruções para usar um pacote de Node.js para executar um servidor de teste simples em sua máquina de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="e3e74-106">The tutorial includes instructions to use a Node.js package to run a simple test server on your development machine.</span></span> <span data-ttu-id="e3e74-107">Se você planeja usar essa opção, você deve ter o [Node.js](https://nodejs.org) instalado em sua máquina de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="e3e74-107">If you plan to use this option, you should have [Node.js](https://nodejs.org) installed on your development machine.</span></span> <span data-ttu-id="e3e74-108">Se você não tiver Node.js, visite o link anterior para opções de download.</span><span class="sxs-lookup"><span data-stu-id="e3e74-108">If you do not have Node.js, visit the previous link for download options.</span></span>

<span data-ttu-id="e3e74-109">Você também deve ter uma conta pessoal da Microsoft com uma caixa de correio no Outlook.com ou uma conta corporativa ou de estudante da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e3e74-109">You should also have either a personal Microsoft account with a mailbox on Outlook.com, or a Microsoft work or school account.</span></span> <span data-ttu-id="e3e74-110">Se você não tem uma conta da Microsoft, há algumas opções para obter uma conta gratuita:</span><span class="sxs-lookup"><span data-stu-id="e3e74-110">If you don't have a Microsoft account, there are a couple of options to get a free account:</span></span>

- <span data-ttu-id="e3e74-111">Você pode [se inscrever para uma nova conta pessoal da Microsoft](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).</span><span class="sxs-lookup"><span data-stu-id="e3e74-111">You can [sign up for a new personal Microsoft account](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).</span></span>
- <span data-ttu-id="e3e74-112">Você pode [se inscrever no programa para desenvolvedores do office 365](https://developer.microsoft.com/office/dev-program) para obter uma assinatura gratuita do Office 365.</span><span class="sxs-lookup"><span data-stu-id="e3e74-112">You can [sign up for the Office 365 Developer Program](https://developer.microsoft.com/office/dev-program) to get a free Office 365 subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="e3e74-113">Este tutorial foi escrito com o nó versão 12.16.1.</span><span class="sxs-lookup"><span data-stu-id="e3e74-113">This tutorial was written with Node version 12.16.1.</span></span> <span data-ttu-id="e3e74-114">As etapas deste guia podem funcionar com outras versões, mas que não foram testadas.</span><span class="sxs-lookup"><span data-stu-id="e3e74-114">The steps in this guide may work with other versions, but that has not been tested.</span></span>

## <a name="feedback"></a><span data-ttu-id="e3e74-115">Comentários</span><span class="sxs-lookup"><span data-stu-id="e3e74-115">Feedback</span></span>

<span data-ttu-id="e3e74-116">Forneça comentários sobre este tutorial no [repositório do GitHub](https://github.com/microsoftgraph/msgraph-training-javascriptspa).</span><span class="sxs-lookup"><span data-stu-id="e3e74-116">Please provide any feedback on this tutorial in the [GitHub repository](https://github.com/microsoftgraph/msgraph-training-javascriptspa).</span></span>
