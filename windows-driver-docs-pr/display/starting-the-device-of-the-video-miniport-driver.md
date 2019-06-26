---
title: ビデオのミニポート ドライバーのデバイスの起動
description: ビデオのミニポート ドライバーのデバイスの起動
ms.assetid: e51a9483-eb12-4f7c-943f-075e670e97b1
keywords:
- ビデオのミニポート ドライバー WDK Windows 2000、デバイスの起動
- ビデオのミニポート ドライバーのデバイスを開始
- デバイス startups WDK のビデオのミニポート
- ビデオのミニポート ドライバー WDK Windows 2000 では、初期化しています
- ビデオのミニポート ドライバーの初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5af495bcee5aa2715a7f1a56904700c954f5ff7c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376052"
---
# <a name="starting-the-device-of-the-video-miniport-driver"></a>ビデオのミニポート ドライバーのデバイスの起動


## <span id="ddk_starting_the_device_of_the_video_miniport_driver_gg"></span><span id="DDK_STARTING_THE_DEVICE_OF_THE_VIDEO_MINIPORT_DRIVER_GG"></span>


PnP マネージャー IRP コードの送信 (を参照してください[IRP の主な機能コード](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-major-function-codes)) グラフィックス アダプターの開始を要求しているビデオ ポート ドライバーにします。 ビデオ ポート ドライバーのディスパッチ ルーチンの呼び出し、ミニポート ドライバーの[ *HwVidFindAdapter* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_find_adapter)この IRP コードへの応答で日常的な。 詳細の一部を*HwVidFindAdapter*のタスクは、次のトピックで説明します。

[ビデオ アダプターへのアクセスの範囲を設定します。](setting-up-video-adapter-access-ranges.md)

[レジストリ内のハードウェア情報の設定](setting-hardware-information-in-the-registry.md)

[アダプターの状態を変更します。](changing-state-on-the-adapter.md)

 

 





