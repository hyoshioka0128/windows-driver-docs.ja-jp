---
title: GDI ベース、モノリシック印刷ドライバーの印刷機能サポート
description: GDI ベース、モノリシック印刷ドライバーの印刷機能サポート
ms.assetid: 4b8116a8-7aee-44cb-9c9d-560662b61073
keywords:
- 印刷機能 WDK、GDI ベースモノリシック印刷ドライバー
- GDI ベースモノリシック印刷ドライバー WDK
- モノリシック印刷ドライバー WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8eb6d1e78739b08ecb87d06702ae89e801128926
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842348"
---
# <a name="print-capabilities-support-in-gdi-based-monolithic-print-drivers"></a>GDI ベース、モノリシック印刷ドライバーの印刷機能サポート


印刷チケットと印刷機能の完全なサポートを提供するには、GPD printer interface DLL を使用できない、GDI ベースのモノリシック印刷ドライバーと[XPSDrv 印刷ドライバー](xpsdrv-printer-drivers.md)が[IPrintTicketProvider インターフェイス](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554375(v=vs.85))を実装する必要があります。 GDI ベースのモノリシック印刷ドライバーは、このインターフェイスをサポートするためには必要ありませんが、PrintCapabilities ドキュメントで公開され、PrintTicket ドキュメントによってサポートされるプリンターの機能が制限される可能性があります。 ただし、XPSDrv 印刷ドライバーは**IPrintTicketProvider**を実装する必要があります。

**注**   Windows 7 では、 **Mxdcgetpdevadjustment**関数に、横方向の回転用の新しいパラメーターがあります。 詳細については、「 [**MxdcXDCGetPDEVAdjustment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mxdc/nf-mxdc-mxdcgetpdevadjustment)」を参照してください。

 

 

 




