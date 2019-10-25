---
title: 印刷機能の Win32 API サポート
description: 印刷機能の Win32 API サポート
ms.assetid: 1b40cc3e-c6f6-460f-b514-4ef3a001f563
keywords:
- 印刷機能 WDK、Win32 API サポート
- DrvDeviceCapabilities
- Win32 アプリケーションの WDK 印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 805009910be2e66e3c554b446d1fa4da8dd12ed8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832109"
---
# <a name="win32-api-support-for-print-capabilities"></a>印刷機能の Win32 API サポート


Windows Vista 印刷サブシステムは、Windows Presentation Foundation (WPF) アプリケーションが GDI ベースの印刷ドライバーを使用できるようにする互換性サポートを提供し、Microsoft Win32 ベースのアプリケーションで XPSDrv 印刷ドライバーを使用できるようにします。 この互換性は、ソフトウェア shim のレイヤーを通じて提供されます。 Shim は、データに対して変換操作を実行するソフトウェアモジュールであり、互換性のないソフトウェアが相互運用できるようにします。 次の図は、印刷機能のためのこの実装のデータパスを示しています。

![印刷機能のデータフローを示す図](images/ptpccomp.gif)

[XPSDrv 印刷ドライバー](xpsdrv-printer-drivers.md)と GDI ベース、バージョン3印刷ドライバーはどちらも、 [**DrvDeviceCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdevicecapabilities)関数をサポートしています。 Win32 アプリケーションが**DrvDeviceCapabilities**または**getdevcap**関数を呼び出すと、印刷サブシステムは**DrvDeviceCapabilities**を呼び出して、印刷ドライバーからデバイスの機能情報を収集します。

WPF アプリケーションが印刷ドライバーから PrintCapabilities ドキュメントを要求すると、印刷サブシステムは次のいずれかの操作を実行します。

-   印刷ドライバーで[IPrintTicketProvider インターフェイス](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554375(v=vs.85))がサポートされている場合、印刷サブシステムは[**IPrintTicketProvider:: GetPrintCapabilities**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554365(v=vs.85))メソッドを使用して、PrintCapabilities ドキュメントの印刷ドライバーを照会します。

-   印刷ドライバーで**IPrintTicketProvider**インターフェイスがサポートされていない場合、印刷チケットマネージャーは印刷ドライバーの[**DrvDeviceCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdevicecapabilities)関数に対してクエリを実行し、返された情報を使用して、アプリケーションに返されます。

Microsoft 印刷ドライバーで**IPrintTicketProvider**インターフェイスをサポートする方法の詳細については、「 [Windows Vista でのプリンタードライバーとプラグインインターフェイスの設計](printer-driver-and-plug-in-helper-interfaces.md)」を参照してください。

 

 




