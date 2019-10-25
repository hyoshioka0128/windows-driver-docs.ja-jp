---
title: DrvAssertMode に応答するデスクトップの切り替え
description: DrvAssertMode に応答するデスクトップの切り替え
ms.assetid: 0e37050f-63db-4e85-840b-c8f817a7f0e8
keywords:
- ディスプレイドライバー WDK Windows 2000、デスクトップ管理
- デスクトップ管理 WDK Windows 2000 ディスプレイ
- デスクトップを切り替える WDK Windows 2000 ディスプレイ
- DrvAssertMode
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7f4c7b319cda7ca5263e3eb15ad172cb27d281c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825518"
---
# <a name="switching-desktops-responding-to-drvassertmode"></a>デスクトップの切り替え: DrvAssertMode への応答


## <span id="ddk_switching_desktops_responding_to_drvassertmode_gg"></span><span id="DDK_SWITCHING_DESKTOPS_RESPONDING_TO_DRVASSERTMODE_GG"></span>


ウィンドウマネージャーを使用すると、画面上のデスクトップを切り替えるときに、デスクトップが正しく再描画され、マウスポインターが有効になり、正しい位置に表示されます。 ディスプレイドライバーは、デスクトップスイッチがある場合にのみ[**DrvAssertMode**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvassertmode)への呼び出しを受信します。

この関数が呼び出されると、ドライバーは、指定された*Pdev*が、pdev の作成時に指定されたモードであるか、テキストモードであるかを確認します。 ウィンドウマネージャーは、正しいポインター形状を選択し、現在位置に移動します。 ドライバーではなく GDI は、マウスポインターの状態を維持します。

GDI は、 *DrvAssertMode*を呼び出して、指定したハードウェアデバイスのモードを設定します。 この関数は、ディスプレイドライバーによって定義された PDEV 構造が作成されたときに指定されたモード、またはハードウェアの既定のモードを選択します。 ドライバーは、PDEV の現在のモードの記録を保持する必要があります。

また、GDI は[**DrvAssertMode**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvassertmode)を呼び出します。 enable パラメーターが**FALSE**に設定されている場合、ユーザーがウィンドウアプリケーションから*x*86 アプリケーションの全画面表示アプリケーションに切り替えるとき、またはユーザーがデスクトップを (すべてのプラットフォームで) 切り替えるときに、が呼び出されます。 ディスプレイドライバーは、ビデオミニポートドライバーへの[**EngDeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdeviceiocontrol)呼び出しで[**IOCTL\_ビデオ\_リセット\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_reset_device)を送信することで、ビデオハードウェアを既定のモードに復元する必要があります。

 

 





