---
title: モノリシック、GDI ベースのプリンター ドライバーでの印刷機能のサポート
description: モノリシック、GDI ベースのプリンター ドライバーでの印刷機能のサポート
ms.assetid: 4b8116a8-7aee-44cb-9c9d-560662b61073
keywords:
- 機能の WDK、GDI ベースのモノリシック印刷ドライバーの印刷します。
- GDI ベース モノリシック印刷ドライバー WDK
- モノリシック印刷ドライバー WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a0d339396d0e671b55017365c5f59f2161be105
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539005"
---
# <a name="print-capabilities-support-in-gdi-based-monolithic-print-drivers"></a>モノリシック、GDI ベースのプリンター ドライバーでの印刷機能のサポート


印刷チケットを完了して、印刷機能のサポートに提供する GDI ベース、モノリシックなプリンター ドライバーと[XPSDrv プリンター ドライバー](xpsdrv-printer-drivers.md) GPD プリンター インターフェイスが DLL を実装する必要がありますを使用することはできません、 [IPrintTicketProviderインターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff554375)します。 モノリシック、GDI ベースのプリンター ドライバーは、この PrintCapabilities ドキュメントで公開され、PrintTicket ドキュメントでサポートされているプリンターの機能を制限する可能性がありますが、このインターフェイスをサポートする必要はありません。 ただし、XPSDrv プリンター ドライバーを実装する必要があります**IPrintTicketProvider**します。

**注**   For Windows 7、 **MxdcGetPDEVAdjustment**関数には、横置きに回転の新しいパラメーター。 詳細については、次を参照してください。 [ **MxdcXDCGetPDEVAdjustment**](https://msdn.microsoft.com/library/windows/hardware/ff557558)します。

 

 

 




