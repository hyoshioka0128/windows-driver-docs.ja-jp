---
title: デスクトップ DrvAssertMode への応答の切り替え
description: デスクトップ DrvAssertMode への応答の切り替え
ms.assetid: 0e37050f-63db-4e85-840b-c8f817a7f0e8
keywords:
- ディスプレイ ドライバー WDK Windows 2000 では、デスクトップ管理
- デスクトップ管理 WDK Windows 2000 の表示
- 切り替えデスクトップ WDK Windows 2000 を表示します。
- DrvAssertMode
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf78008581321bfb1eafb9c8ea808f9fdf54d697
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372054"
---
# <a name="switching-desktops-responding-to-drvassertmode"></a>デスクトップの切り替え: DrvAssertMode への応答


## <span id="ddk_switching_desktops_responding_to_drvassertmode_gg"></span><span id="DDK_SWITCHING_DESKTOPS_RESPONDING_TO_DRVASSERTMODE_GG"></span>


ディスプレイにデスクトップを切り替え、デスクトップが正しく再描画されると、マウス ポインターが有効化され、正しい位置に表示されるウィンドウ マネージャーによって確認されます。 ディスプレイ ドライバーへの呼び出しを受信する[ **DrvAssertMode** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvassertmode)デスクトップ スイッチがある場合にのみです。

この関数が呼び出されると、ドライバーにより、指定された*PDEV* PDEV を作成したときに指定されたモードまたはテキスト モードでは、します。 ウィンドウ マネージャーは、正しいポインターの形を選択し、現在の位置に移動します。 GDI やドライバーではなく、マウス ポインターの状態を維持する責任を負います。

GDI 呼び出し*DrvAssertMode*指定されたハードウェア デバイスのモードに設定します。 この関数は、ディスプレイ ドライバー定義 PDEV 構造の作成時に指定されたモードまたはハードウェアの既定のモードのいずれかを選択します。 ドライバーは、PDEV の現在のモードのレコードを保持する必要があります。

GDI の呼び出しも[ **DrvAssertMode**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvassertmode)、有効にするパラメーターを設定して**FALSE**で全画面表示、アプリケーションにウィンドウを持つアプリケーションからユーザーが切り替えると、*x*86 アプリケーションは、(すべてのプラットフォーム) で、ユーザーがデスクトップを切り替える場合またはします。 ディスプレイ ドライバーは送信することによって、既定のモードにビデオ ハードウェアを復元する必要があります[ **IOCTL\_ビデオ\_リセット\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_reset_device)で、 [ **EngDeviceIoControl** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdeviceiocontrol)ビデオのミニポート ドライバーに呼び出します。

 

 





