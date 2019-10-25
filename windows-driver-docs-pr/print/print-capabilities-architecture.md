---
title: 印刷機能アーキテクチャ
description: 印刷機能アーキテクチャ
ms.assetid: d19438ca-8c88-4835-8445-2799387e0912
keywords:
- 印刷機能 WDK、アーキテクチャ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37930b47503186ce6fba466b166224f108772227
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842352"
---
# <a name="print-capabilities-architecture"></a>印刷機能アーキテクチャ


PrintCapabilities オブジェクトは、 [IPrintTicketProvider インターフェイス](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554375(v=vs.85))の印刷ドライバーの実装の[**IPrintTicketProvider:: GetPrintCapabilities**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554365(v=vs.85))メソッドによって返されます。 XPSDrv 印刷ドライバーは、 [**DrvDeviceCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdevicecapabilities)関数に加えて IPrintTicketProvider インターフェイスを実装する必要があります。

古い GDI ベースの印刷ドライバーを変更して PrintCapabilities ドキュメントを直接提供することはできますが、この変更は必要ありません。 Windows Vista の印刷サブシステムでは、GDI ベースのドライバー用の XML PrintCapabilities ドキュメントが作成されますが、それを返す機能は追加されません。 ただし、Windows Vista の印刷サブシステムによって作成される PrintCapabilities ドキュメントには、Microsoft Win32 関数**DeviceCapabilities**がサポートするパラメーターの限られたセットのみが含まれています。 GDI ベースの印刷ドライバーで、プリンターの機能の完全な一覧を提供するには、 [IPrintTicketProvider インターフェイス](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554375(v=vs.85))のサポートが含まれている必要があります。

次の一覧と図は、さまざまな種類の印刷ドライバーが印刷機能テクノロジをどのようにサポートしているかを示しています。

<a href="" id="unidrv-or-pscript5-print-driver"></a>Unidrv または PScript5 印刷ドライバー  
[IPrintTicketProvider インターフェイス](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554375(v=vs.85))は、Windows Vista の Universal (Unidrv) および PostScript (PScript5) 印刷ドライバーに追加されました。

<a href="" id="unidrv-or-pscript5-print-driver-plug-in"></a>Unidrv または PScript5 印刷ドライバープラグイン  
カスタム機能がインストールされている Unidrv および Pscript5 印刷ドライバーには、機能を追加または削除し、正確な PrintCapabilities ドキュメントを返すためのプラグインが必要です。 Unidrv および PScript5 印刷ドライバー用のカスタム機能プラグインでは、 [IPrintOemPrintTicketProvider インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintoemprintticketprovider)がサポートされている必要があります。

<a href="" id="-monolithic-gdi-based-and-xpsdrv-print-drivers"></a>モノリシック GDI ベースおよび XPSDrv 印刷ドライバー  
XPSDrv 印刷ドライバーは、 [IPrintTicketProvider インターフェイス](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554375(v=vs.85))をサポートしている必要があります。 GDI ベースのモノリシック印刷ドライバーは、IPrintTicketProvider インターフェイスをサポートして、Win32 関数**DeviceCapabilities**では提供されないプリンターの機能と機能を返す必要があります。

![印刷ドライバーでの印刷機能のサポートを示す図](images/ptpcarch1.gif)

 

 




