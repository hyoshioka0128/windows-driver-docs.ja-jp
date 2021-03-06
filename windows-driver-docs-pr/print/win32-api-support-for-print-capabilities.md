---
title: 印刷機能の Win32 API サポート
description: 印刷機能の Win32 API サポート
ms.assetid: 1b40cc3e-c6f6-460f-b514-4ef3a001f563
keywords:
- 印刷機能の WDK、Win32 API のサポート
- DrvDeviceCapabilities
- WDK の Win32 アプリケーションを印刷します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8bc1c3fc6afccf301ab2e2709a88fcbd7573d84e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368971"
---
# <a name="win32-api-support-for-print-capabilities"></a>印刷機能の Win32 API サポート


Windows Vista の印刷サブシステムを GDI ベースの印刷ドライバーを使用する Windows Presentation Foundation (WPF) アプリケーションと可能 XPSDrv プリンター ドライバーを使用する Microsoft Win32 ベースのアプリケーションの互換性サポートを提供します。 この互換性は、ソフトウェアの shim のレイヤーによって提供されます。 Shim とは、互換性のないソフトウェアがそれ以外の場合と相互運用できるように、データに対する変換操作を実行するソフトウェア モジュールです。 次の図は、この印刷機能の実装のデータ パスを示します。

![印刷機能のデータ フローを示す図](images/ptpccomp.gif)

両方[XPSDrv プリンター ドライバー](xpsdrv-printer-drivers.md)と GDI ベースのバージョン 3 の印刷ドライバーのサポート、 [ **DrvDeviceCapabilities** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvdevicecapabilities)関数。 Win32 アプリケーションを呼び出すと**DrvDeviceCapabilities**または**GetDevCap**関数、印刷サブシステムが呼び出す**DrvDeviceCapabilities**デバイスを収集するにはプリンター ドライバーから機能情報。

WPF アプリケーションを要求すると、PrintCapabilities ドキュメントを印刷ドライバーから印刷サブシステムは、次のいずれかには。

-   印刷ドライバーがサポートしている場合、 [IPrintTicketProvider インターフェイス](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554375(v=vs.85))、印刷サブシステムを使用して PrintCapabilities ドキュメントの印刷ドライバーをクエリは、 [ **IPrintTicketProvider:。GetPrintCapabilities** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554365(v=vs.85))メソッド。

-   印刷ドライバーがサポートされていない場合、 **IPrintTicketProvider**インターフェイス、チケットのプリント マネージャーは照会、 [ **DrvDeviceCapabilities** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvdevicecapabilities)印刷の関数ドライバーとアプリケーションに返される PrintTicket ドキュメントを作成する返される情報を使用します。

方法の詳細については**IPrintTicketProvider**インターフェイスが Microsoft の印刷ドライバーによってサポートされているを参照してください[プリンター ドライバーと Windows Vista のプラグイン インターフェイスのデザイン](printer-driver-and-plug-in-helper-interfaces.md)します。

 

 




