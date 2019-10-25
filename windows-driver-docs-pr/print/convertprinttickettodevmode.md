---
title: ConvertPrintTicketToDevMode 概要
description: 'アプリケーションの渡された印刷チケットからの IPrintOemPrintTicketProvider:: ConvertPrintTicketToDevMode メソッドの使用法について説明します。'
ms.assetid: dd77d79e-e274-47c3-9bfd-95054bc9f23d
keywords:
- ConvertPrintTicketToDevMode
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc6c309d8a6f38d21f2f309cd26234772c65350e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831813"
---
# <a name="convertprinttickettodevmode-overview"></a>ConvertPrintTicketToDevMode 概要


Unidrv および PScript5 印刷ドライバーは、アプリケーションの ConvertPrintTicketToDevMode への呼び出しで渡された印刷チケットの情報を使用して、サポートする[**Devmodew**](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)構造体の公開部分とプライベート部分を入力します。 [**IPrintOemPrintTicketProvider:: ConvertPrintTicketToDevMode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemprintticketprovider-convertprinttickettodevmode)メソッドは、インストールされた各印刷ドライバープラグインに対して呼び出されます。

次の図は、ドライバーが**ConvertPrintTicketToDevMode**を呼び出すときの**IPrintOemPrintTicketProvider:: ConvertPrintTicketToDevMode**への呼び出しの順序を示しています。

![convertprinttickettodevmode 呼び出しシーケンスを示す図](images/ptpcpt2dm-uml.gif)





