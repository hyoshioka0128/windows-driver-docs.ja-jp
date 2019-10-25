---
title: ビデオのミニポート ドライバーのデバイスの起動
description: ビデオのミニポート ドライバーのデバイスの起動
ms.assetid: e51a9483-eb12-4f7c-943f-075e670e97b1
keywords:
- ビデオミニポートドライバー WDK Windows 2000、開始デバイス
- ビデオミニポートドライバーのデバイスを起動しています
- デバイスのスタートアップ WDK ビデオミニポート
- ビデオミニポートドライバー WDK Windows 2000、初期化
- ビデオミニポートドライバーの初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 32eeace79229ead28a6a6dfdee4a1a4701fefddf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825706"
---
# <a name="starting-the-device-of-the-video-miniport-driver"></a>ビデオのミニポート ドライバーのデバイスの起動


## <span id="ddk_starting_the_device_of_the_video_miniport_driver_gg"></span><span id="DDK_STARTING_THE_DEVICE_OF_THE_VIDEO_MINIPORT_DRIVER_GG"></span>


PnP マネージャーは、グラフィックスアダプターの起動を要求する IRP コード ( [irp の主要な関数コード](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-major-function-codes)を参照) をビデオポートドライバーに送信します。 ビデオポートドライバーのディスパッチルーチンは、この IRP コードに応答して、ミニポートドライバーの[*HwVidFindAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_find_adapter)ルーチンを呼び出します。 いくつかの*HwVidFindAdapter*のタスクの詳細については、次のトピックで説明します。

[ビデオアダプターのアクセス範囲の設定](setting-up-video-adapter-access-ranges.md)

[レジストリでのハードウェア情報の設定](setting-hardware-information-in-the-registry.md)

[アダプターの状態の変更](changing-state-on-the-adapter.md)

 

 





