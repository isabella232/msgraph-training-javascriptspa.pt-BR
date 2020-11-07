---
ms.openlocfilehash: bbb1dd429dca4e67735c5fdb2b2280f729115eb2
ms.sourcegitcommit: 18785a430bc1885ccac1ebbe1f3eba634c58bea8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/30/2020
ms.locfileid: "48822757"
---
<!-- markdownlint-disable MD002 MD041 -->

Este tutorial ensina como criar um aplicativo JavaScript de página única que usa a API do Microsoft Graph para recuperar informações de calendário de um usuário.

> [!TIP]
> Se preferir baixar o tutorial concluído, você poderá baixar ou clonar o repositório do [GitHub](https://github.com/microsoftgraph/msgraph-training-javascriptspa).

## <a name="prerequisites"></a>Pré-requisitos

Antes de iniciar este tutorial, você precisará de acesso a um servidor HTTP para hospedar os arquivos de amostra. Pode ser um servidor de teste no seu computador de desenvolvimento ou um servidor remoto. O tutorial inclui instruções para usar um pacote de Node.js para executar um servidor de teste simples em sua máquina de desenvolvimento. Se você planeja usar essa opção, você deve ter o [Node.js](https://nodejs.org) instalado em sua máquina de desenvolvimento. Se você não tiver Node.js, visite o link anterior para opções de download.

Você também deve ter uma conta pessoal da Microsoft com uma caixa de correio no Outlook.com ou uma conta corporativa ou de estudante da Microsoft. Se você não tem uma conta da Microsoft, há algumas opções para obter uma conta gratuita:

- Você pode [se inscrever para uma nova conta pessoal da Microsoft](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).
- Você pode [se inscrever no programa para desenvolvedores do office 365](https://developer.microsoft.com/office/dev-program) para obter uma assinatura gratuita do Office 365.

> [!NOTE]
> Este tutorial foi escrito com o nó versão 12.16.1. As etapas deste guia podem funcionar com outras versões, mas que não foram testadas.

## <a name="feedback"></a>Comentários

Forneça comentários sobre este tutorial no [repositório do GitHub](https://github.com/microsoftgraph/msgraph-training-javascriptspa).
