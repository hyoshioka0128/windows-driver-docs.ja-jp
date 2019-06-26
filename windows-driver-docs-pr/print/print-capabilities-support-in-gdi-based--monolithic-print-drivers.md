---
title: GDI ベース、モノリシック印刷ドライバーの印刷機能サポート
description: GDI ベース、モノリシック印刷ドライバーの印刷機能サポート
ms.assetid: 4b8116a8-7aee-44cb-9c9d-560662b61073
keywords:
- 機能の WDK、GDI ベースのモノリシック印刷ドライバーの印刷します。
- GDI ベース モノリシック印刷ドライバー WDK
- モノリシック印刷ドライバー WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b5c54fd18698245d922e368cfff840864249a5c2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373769"
---
# <a name="print-capabilities-support-in-gdi-based-monolithic-print-drivers"></a>GDI ベース、モノリシック印刷ドライバーの印刷機能サポート


印刷チケットを完了して、印刷機能のサポートに提供する GDI ベース、モノリシックなプリンター ドライバーと[XPSDrv プリンター ドライバー](xpsdrv-printer-drivers.md) GPD プリンター インターフェイスが DLL を実装する必要がありますを使用することはできません、 [IPrintTicketProviderインターフェイス](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554375(v=vs.85))します。 モノリシック、GDI ベースのプリンター ドライバーは、この PrintCapabilities ドキュメントで公開され、PrintTicket ドキュメントでサポートされているプリンターの機能を制限する可能性がありますが、このインターフェイスをサポートする必要はありません。 ただし、XPSDrv プリンター ドライバーを実装する必要があります**IPrintTicketProvider**します。

**注**   For Windows 7、 **MxdcGetPDEVAdjustment**関数には、横置きに回転の新しいパラメーター。 詳細については、次を参照してください。 [ **MxdcXDCGetPDEVAdjustment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mxdc/nf-mxdc-mxdcgetpdevadjustment)します。

 

 

 




