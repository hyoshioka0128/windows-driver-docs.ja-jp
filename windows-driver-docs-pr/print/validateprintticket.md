---
title: ValidatePrintTicket 概要
description: '各プラグインは、IPrintOemPrintTicketProvider:: ValidatePrintTicket メソッドを呼び出して、PrintTicket を検証します。'
ms.assetid: 3a4cf946-c931-4f71-9f1a-4efec4dfe866
keywords:
- ValidatePrintTicket
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a528f89f55339e656024eaf417c248dca398453b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844757"
---
# <a name="validateprintticket-overview"></a>ValidatePrintTicket 概要


Unidrv および PScript5 印刷ドライバーは、次の図とリストに示されているシーケンスを使用して、印刷チケットを検証します。

![unidrv および pscript5 印刷ドライバーで印刷チケットを検証する方法を示す図](images/ptpcvalpt-uml.gif)

1.  各プラグインに対して、 [**IPrintOemPrintTicketProvider:: ExpandIntentOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemprintticketprovider-expandintentoptions)メソッドを呼び出します。

2.  [**IPrintOemPrintTicketProvider:: ConvertPrintTicketToDevMode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemprintticketprovider-convertprinttickettodevmode)メソッドを呼び出します。

3.  各プラグインに対して**IPrintOemPrintTicketProvider:: ConvertPrintTicketToDevMode**を呼び出して、 [**devmodew**](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)構造体のプライベート部分を変換します。

4.  Unidrv または PScript5 print driver がサポートする DEVMODEW 構造の公開部分とプライベート部分を検証します。

5.  各プラグインについて、DEVMODEW 構造体のプライベートパートを検証します。

6.  [**IPrintTicketProvider:: ConvertPrintTicketToDevMode**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554363(v=vs.85))メソッドを呼び出します。

7.  各プラグインに対して、 [**IPrintOemPrintTicketProvider:: ConvertDevModeToPrintTicket**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff553161(v=vs.85))メソッドを呼び出して、DEVMODEW 構造体のプライベート部分を変換します。

8.  各プラグインに対して、 [**IPrintOemPrintTicketProvider:: ValidatePrintTicket**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff553184(v=vs.85))メソッドを呼び出して、PrintTicket を検証します。

 

 




