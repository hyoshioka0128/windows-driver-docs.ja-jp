---
title: IDE ミニドライバー ルーチンの初期化と呼び出し
description: IDE ミニドライバー ルーチンの初期化と呼び出し
ms.assetid: ae7b19a9-0a2e-4231-b008-879b7f6c8566
keywords:
- IDE コント ローラー ミニドライバー WDK のストレージの初期化
- IDE コント ローラー ミニドライバー WDK、ストレージの初期化
- IDE コント ローラー ミニドライバー WDK ストレージ、呼び出し元
- IDE コント ローラー ミニドライバー WDK のストレージ、呼び出し元
- IDE コント ローラーのミニドライバーの初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b1dc53fdf3def48510d4e96d2eaaf6ec4d32a99
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370451"
---
# <a name="initializing-and-calling-ide-minidriver-routines"></a>IDE ミニドライバー ルーチンの初期化と呼び出し


## <span id="ddk_initializing_and_calling_ide_minidriver_routines_kr"></span><span id="DDK_INITIALIZING_AND_CALLING_IDE_MINIDRIVER_ROUTINES_KR"></span>


IDE コント ローラーのすべてのミニドライバーは、一連のハードウェア固有の機能を実装する標準のルーチンを提供する必要があります。 次の図は、方法、IDE コント ローラーのミニドライバーのルーチンを使用できるように、コント ローラー用ドライバーを示します。 PciIdeX ライブラリが概念的には、次の図に示すように IDE コント ローラーのドライバーから独立した内に含まれるコント ローラーのドライバーの実行可能ファイルに注意してください。 *pciidex.sys*します。 ミニドライバー PciIdeX ライブラリ ルーチンを呼び出す場合は、コント ローラー ドライバー内でルーチンを実際に呼び出します。

![ミニドライバーの日常的な初期化のためのプログラム フロー](images/idecallbacks.png)

1.  ミニドライバーの IDE コント ローラー ドライバー、PnP マネージャー ロードを呼び出してその[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)ルーチン、コント ローラーのドライバーのドライバー オブジェクトへのポインターを渡します。

2.  ミニドライバーの**DriverEntry**呼び出し、 [ **PciIdeXInitialize** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff563788(v=vs.85))ライブラリ ルーチン、ミニドライバーにポインターを渡す**GetControllerProperties**ルーチン。

3.  **PciIdeXInitialize**へのポインターを格納**GetControllerProperties**ドライバー オブジェクト。

4.  PnP マネージャー ディスパッチ IRP\_MN\_開始\_IDE コント ローラーのドライバーのデバイス要求コント ローラーを起動します。 IDE コント ローラーのドライバーで要求を受け取ると、 [ **DispatchPnP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン、デバイスを開始する内部のルーチンを呼び出すとします。

5.  コント ローラー ドライバーへのポインターを取得する**GetControllerProperties**ドライバー オブジェクトに格納されています。

6.  コント ローラーのドライバー呼び出し**GetControllerProperties**へのポインターを渡して、 [ **IDE\_コント ローラー\_プロパティ**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559076(v=vs.85))構造体。

7.  **GetControllerProperties**ミニドライバー ルーチンの標準的な一連のポインターを IDE に読み込み\_コント ローラー\_プロパティ。

ミニドライバーは、IDE を設定すると\_コント ローラー\_ミニドライバーのルーチンを指す関数ポインターのプロパティが構造体、コント ローラー ドライバーが呼び出すことができます。

呼び出すコント ローラーのすべてのミニドライバーを提供する必要があるルーチンは次のとおりです。

このルーチンは、指定されたチャネルが有効になっているかどうかを判断します。

このルーチンは、IDE コント ローラーのハードウェアのプロパティを報告します。

このルーチンは、そのコント ローラーの両方のチャンネルを一度にアクセスできるかどうかを示します。

このルーチンを返します、最適なモードと DMA のベスト モードで提示されている各デバイスを*XferMode*します。

このルーチンでは、あり超ダイレクト メモリ アクセス (UDMA) の転送モードが現在、デバイスの最適なことを示します。

このルーチンは、DMA を使用して I/O を実行できるかどうかを判断します。

[**HwIdeXChannelEnabled**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557252(v=vs.85))

[**HwIdeXGetControllerProperties**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557254(v=vs.85))

[**HwIdeXSyncAccessRequired**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557256(v=vs.85))

[**HwIdeXTransferModeSelect**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557260(v=vs.85))

[**HwIdeXUdmaModesSupported**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557264(v=vs.85))

[**HwIdeXUseDma**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557266(v=vs.85))

 

 




