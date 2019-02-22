---
title: 印刷機能のアーキテクチャ
description: 印刷機能のアーキテクチャ
ms.assetid: d19438ca-8c88-4835-8445-2799387e0912
keywords:
- 印刷機能の WDK、アーキテクチャ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9102e16108f775a56d438b3be2aea97396d2be7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550429"
---
# <a name="print-capabilities-architecture"></a>印刷機能のアーキテクチャ


PrintCapabilities オブジェクトは、によって返される、 [ **IPrintTicketProvider::GetPrintCapabilities** ](https://msdn.microsoft.com/library/windows/hardware/ff554365)の印刷ドライバーの実装のメソッド、 [IPrintTicketProvider インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff554375). XPSDrv プリンター ドライバーは、ほかに IPrintTicketProvider インターフェイスを実装する必要があります、 [ **DrvDeviceCapabilities** ](https://msdn.microsoft.com/library/windows/hardware/ff548539)関数。

PrintCapabilities ドキュメントを直接がこの変更は必要ありませんを提供する、古い GDI ベースの印刷ドライバーを変更することができます。 Windows Vista の印刷サブシステムは、GDI ベースのドライバーを 1 つを返す機能を追加しないでくださいを対象とした XML PrintCapabilities ドキュメントを作成します。 PrintCapabilities ドキュメント Windows Vista の印刷サブシステムを作成、ただし、には制限付きのパラメーターのセットのみが含まれている Microsoft Win32 関数**DeviceCapabilities**をサポートしています。 GDI ベース印刷ドライバーのプリンターの機能と機能の完全な一覧を提供する、サポートを含めることは、 [IPrintTicketProvider インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff554375)します。

次の一覧と図は、印刷ドライバーのさまざまな種類が、印刷機能のテクノロジをサポートする方法を説明します。

<a href="" id="unidrv-or-pscript5-print-driver"></a>Unidrv または PScript5 の印刷ドライバー  
[IPrintTicketProvider インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff554375)に追加されましたユニバーサル (Unidrv) および PostScript (PScript5) 印刷ドライバーでは、Windows Vista です。

<a href="" id="unidrv-or-pscript5-print-driver-plug-in"></a>Unidrv または PScript5 印刷ドライバー プラグイン  
Unidrv と Pscript5 プラグインを追加または削除の機能を必要とし、正確な PrintCapabilities ドキュメントを返すカスタムの機能のドライバーを印刷します。 カスタム、Unidrv と印刷ドライバーをサポートする必要があります PScript5 のプラグインを特徴と、 [IPrintOemPrintTicketProvider インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff553174)します。

<a href="" id="-monolithic-gdi-based-and-xpsdrv-print-drivers"></a> GDI ベース モノリシックと XPSDrv プリンター ドライバー  
XPSDrv プリンター ドライバーをサポートする必要があります、 [IPrintTicketProvider インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff554375)します。 モノリシック、GDI ベースのプリンター ドライバーはプリンターの機能を返す IPrintTicketProvider インターフェイスをサポートする必要がありますや機能を Win32 関数**DeviceCapabilities**はできません。

![印刷ドライバーでの印刷機能のサポートを示す図](images/ptpcarch1.gif)

 

 




