---
title: IDE ミニドライバー ルーチンの初期化と呼び出し
description: IDE ミニドライバー ルーチンの初期化と呼び出し
ms.assetid: ae7b19a9-0a2e-4231-b008-879b7f6c8566
keywords:
- IDE コントローラーミニドライバー WDK storage、初期化
- ストレージ IDE コントローラーミニドライバー WDK、初期化中
- IDE コントローラーミニドライバー WDK storage、呼び出し
- storage IDE controller ミニドライバー WDK、呼び出し
- IDE コントローラーミニドライバーを初期化しています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b689bbd9666ffcbf5f0c6fb6a9deb352cda8044b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845378"
---
# <a name="initializing-and-calling-ide-minidriver-routines"></a>IDE ミニドライバー ルーチンの初期化と呼び出し


## <span id="ddk_initializing_and_calling_ide_minidriver_routines_kr"></span><span id="DDK_INITIALIZING_AND_CALLING_IDE_MINIDRIVER_ROUTINES_KR"></span>


すべての IDE コントローラーミニドライバーは、ハードウェア固有の機能を実装する一連の標準ルーチンを提供する必要があります。 次の図は、IDE コントローラーミニドライバーがコントローラードライバーでルーチンを使用できるようにする方法を示しています。 PciIdeX ライブラリは、次の図に示すように、概念的には IDE コントローラードライバーから分離されていますが、コントローラードライバーの実行可能ファイル*PciIdeX*に含まれています。 ミニドライバーが PciIdeX ライブラリルーチンを呼び出すと、実際には、コントローラードライバー内のルーチンが呼び出されます。

![ミニドライバールーチン初期化のプログラムフロー](images/idecallbacks.png)

1.  PnP マネージャーは、IDE コントローラードライバーミニドライバーを読み込み、その[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンを呼び出して、コントローラードライバーのドライバーオブジェクトへのポインターを渡します。

2.  ミニドライバーの**Driverentry**は[**PciIdeXInitialize**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff563788(v=vs.85)) library ルーチンを呼び出し、ミニドライバーの**getcontrollerproperties**ルーチンへのポインターを渡します。

3.  **PciIdeXInitialize**は、 **getコントローラープロパティ**へのポインターを driver オブジェクトに格納します。

4.  PnP マネージャーは、コントローラーを起動するために、\_デバイスの要求を IDE コントローラードライバーに開始する\_、IRP\_をディスパッチします。 IDE コントローラードライバーは、 [**DispatchPnP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンで要求を受信し、デバイスを起動する内部ルーチンを呼び出します。

5.  コントローラードライバーは、ドライバーオブジェクトに格納されている**Getcontroller プロパティ**へのポインターを取得します。

6.  コントローラードライバーは、 **Getcontroller プロパティ**を呼び出して、 [**IDE\_controller\_properties**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559076(v=vs.85))構造体へのポインターを渡します。

7.  **Getcontroller プロパティ**は、標準セットのミニドライバールーチンのポインターを IDE\_CONTROLLER\_のプロパティに読み込みます。

ミニドライバーは、ミニドライバーのルーチンを指す関数ポインターを使用して、IDE\_\_CONTROLLER のプロパティ構造を設定すると、コントローラードライバーはそれらを呼び出すことができます。

すべてのミニドライバーがコントローラーに対してを呼び出すために提供する必要があるルーチンは次のとおりです。

このルーチンは、指定されたチャネルが有効かどうかを判断します。

このルーチンは、IDE コントローラーのハードウェアのプロパティを報告します。

このルーチンは、コントローラーの両方のチャネルに一度にアクセスできるかどうかを示します。

このルーチンは、 *Xのモード*で示されている各デバイスに最適な PIO モードと最適な DMA モードを返します。

このルーチンは、どのウルトラダイレクトメモリアクセス (UDMA) 転送モードが最新であり、デバイスに最適であるかを示します。

このルーチンは、DMA を使用して i/o を実行できるかどうかを判断します。

[**HwIdeXChannelEnabled**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557252(v=vs.85))

[**HwIdeXGetControllerProperties**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557254(v=vs.85))

[**HwIdeXSyncAccessRequired**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557256(v=vs.85))

[**HwIdeXTransferModeSelect**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557260(v=vs.85))

[**HwIdeXUdmaModesSupported**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557264(v=vs.85))

[**HwIdeXUseDma**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557266(v=vs.85))

 

 




