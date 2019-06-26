---
title: モノリシック印刷ドライバーに印刷チケット サポートを追加する
description: モノリシック印刷ドライバーに印刷チケット サポートを追加する
ms.assetid: 82c65b9a-6e7b-4acd-93aa-33d696ddc421
keywords:
- プリンター インターフェイス DLL の WDK、印刷チケットのサポート
- モノリシック印刷ドライバー WDK
- チケットの WDK、モノリシックの印刷ドライバーを印刷します。
- IPrintTicketProvider
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa4b3b4550eed074635933317951a291c23a46bc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382593"
---
# <a name="adding-print-ticket-support-to-monolithic-print-drivers"></a>モノリシック印刷ドライバーに印刷チケット サポートを追加する


印刷チケットを提供する場合は、モノリシック印刷ドライバーのサポート、サポート、[印刷チケットと印刷機能テクノロジ](print-ticket-and-print-capabilities-technologies.md)、それを実装する必要があります、 [IPrintTicketProvider インターフェイス](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554375(v=vs.85))とも印刷ドライバーによって使用される COM スタイルの呼び出し元メソッドのために必要な IClassFactory インターフェイスのサポートを提供します。 ドライバーには、少なくとも、ようになりました中に呼び出される IPrintTicketProvider インターフェイスのメソッドをサポートする必要がありますの下に示す順序で呼び出します。

1.  [GetSupportedVersions](getsupportedversions.md)

2.  [BindPrinter](bindprinter.md)

3.  [QueryDeviceNamespace](querydevicenamespace.md)

このインターフェイスのサポートを完了するには、印刷ドライバーが IPrintTicketProvider インターフェイスのメソッドの残りの部分をサポートする必要があります。

[GetPrintCapabilities](getprintcapabilities.md)

[ConvertDevModeToPrintTicket](convertdevmodetoprintticket2.md)

[ConvertPrintTicketToDevMode](convertprinttickettodevmode.md)

[ValidatePrintTicket](validateprintticket.md)

 

 




