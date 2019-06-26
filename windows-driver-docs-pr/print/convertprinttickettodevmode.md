---
title: ConvertPrintTicketToDevMode 概要
description: アプリケーションの印刷チケットの渡されたから IPrintOemPrintTicketProvider::ConvertPrintTicketToDevMode メソッドの使用状況をについて説明します。
ms.assetid: dd77d79e-e274-47c3-9bfd-95054bc9f23d
keywords:
- ConvertPrintTicketToDevMode
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1be0b61b03044ff5e24f193f1844db38f4abdc6a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372474"
---
# <a name="convertprinttickettodevmode-overview"></a>ConvertPrintTicketToDevMode 概要


Unidrv と PScript5 印刷ドライバーをパブリックおよびプライベートな部分の入力、 [ **DEVMODEW** ](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)から渡されたアプリケーションの印刷チケット情報を使用してサポートされる構造体ConvertPrintTicketToDevMode を呼び出します。 [ **IPrintOemPrintTicketProvider::ConvertPrintTicketToDevMode** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemprintticketprovider-convertprinttickettodevmode)各印刷ドライバーのプラグインがインストールされているメソッドが呼び出されます。

次の図への呼び出しの順序**IPrintOemPrintTicketProvider::ConvertPrintTicketToDevMode**ドライバーを呼び出すと**ConvertPrintTicketToDevMode**します。

![呼び出しシーケンス convertprinttickettodevmode を示す図](images/ptpcpt2dm-uml.gif)





