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
ms.openlocfilehash: 5f267349111f0c5059197d720479957a1afc7ab5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342262"
---
# <a name="adding-print-ticket-support-to-monolithic-print-drivers"></a>モノリシック印刷ドライバーに印刷チケット サポートを追加する


印刷チケットを提供する場合は、モノリシック印刷ドライバーのサポート、サポート、[印刷チケットと印刷機能テクノロジ](print-ticket-and-print-capabilities-technologies.md)、それを実装する必要があります、 [IPrintTicketProvider インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff554375)とも印刷ドライバーによって使用される COM スタイルの呼び出し元メソッドのために必要な IClassFactory インターフェイスのサポートを提供します。 ドライバーには、少なくとも、ようになりました中に呼び出される IPrintTicketProvider インターフェイスのメソッドをサポートする必要がありますの下に示す順序で呼び出します。

1.  [GetSupportedVersions](getsupportedversions.md)

2.  [BindPrinter](bindprinter.md)

3.  [QueryDeviceNamespace](querydevicenamespace.md)

このインターフェイスのサポートを完了するには、印刷ドライバーが IPrintTicketProvider インターフェイスのメソッドの残りの部分をサポートする必要があります。

[GetPrintCapabilities](getprintcapabilities.md)

[ConvertDevModeToPrintTicket](convertdevmodetoprintticket2.md)

[ConvertPrintTicketToDevMode](convertprinttickettodevmode.md)

[ValidatePrintTicket](validateprintticket.md)

 

 




