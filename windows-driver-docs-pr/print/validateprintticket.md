---
title: ValidatePrintTicket 概要
description: 各プラグインは、検証、PrintTicket IPrintOemPrintTicketProvider::ValidatePrintTicket メソッドを呼び出します。
ms.assetid: 3a4cf946-c931-4f71-9f1a-4efec4dfe866
keywords:
- ValidatePrintTicket
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67fbaa90896d86d8cde63fd7cea429f181bb6d99
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379105"
---
# <a name="validateprintticket-overview"></a>ValidatePrintTicket 概要


Unidrv と PScript5 の印刷ドライバーでは、次の図と一覧を表示するシーケンスを使用して印刷チケットを検証します。

![unidrv と pscript5 のドライバーを印刷する方法を示すダイアグラムが印刷チケットを検証します。](images/ptpcvalpt-uml.gif)

1.  各プラグインを呼び出し、 [ **IPrintOemPrintTicketProvider::ExpandIntentOptions** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemprintticketprovider-expandintentoptions)メソッド。

2.  呼び出す、 [ **IPrintOemPrintTicketProvider::ConvertPrintTicketToDevMode** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemprintticketprovider-convertprinttickettodevmode)メソッド。

3.  各プラグインは、呼び出し**IPrintOemPrintTicketProvider::ConvertPrintTicketToDevMode**のプライベート部分に変換する、 [ **DEVMODEW** ](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)構造体。

4.  パブリックおよびプライベートな部分を Unidrv または PScript5 印刷ドライバーがサポートする DEVMODEW 構造を検証します。

5.  各プラグイン、DEVMODEW 構造にプライベートな部分を検証します。

6.  呼び出す、 [ **IPrintTicketProvider::ConvertPrintTicketToDevMode** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554363(v=vs.85))メソッド。

7.  各プラグインを呼び出し、 [ **IPrintOemPrintTicketProvider::ConvertDevModeToPrintTicket** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff553161(v=vs.85)) DEVMODEW 構造体のプライベート部分に変換します。

8.  各プラグインを呼び出し、 [ **IPrintOemPrintTicketProvider::ValidatePrintTicket** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff553184(v=vs.85)) PrintTicket を検証するメソッド。

 

 




