---
title: 電源管理とビデオのミニポート ドライバー (XDDM) での PnP
description: ビデオ ミニポート ドライバーでの電源管理およびプラグ アンド プレイ (Windows 2000 モデル)
ms.assetid: e5b2ac53-e492-43de-91a3-5b02c26ee9a3
keywords:
- ビデオのミニポート ドライバー WDK Windows 2000 では、プラグ アンド プレイ
- ビデオのミニポート ドライバー WDK Windows 2000 では、電源管理
- プラグ アンド プレイ WDK ビデオのミニポート
- PnP WDK ビデオのミニポート
- 電源管理 WDK ビデオのミニポート
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: bc1927b4acd18fcfca7bcee6d65e7edff0a6d708
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365710"
---
# <a name="power-management-and-plug-and-play-in-video-miniport-drivers-windows-2000-model"></a>ビデオ ミニポート ドライバーでの電源管理およびプラグ アンド プレイ (Windows 2000 モデル)


## <span id="ddk_plug_and_play_and_power_management_in_video_miniport_drivers_windo"></span><span id="DDK_PLUG_AND_PLAY_AND_POWER_MANAGEMENT_IN_VIDEO_MINIPORT_DRIVERS_WINDO"></span>


すべての Windows 2000 およびそれ以降のミニポート ドライバーには、プラグ アンド プレイと電源管理をサポートする必要があります。 などの子デバイスを列挙する機能が含まれます*DDC*モニタ、間統合の回線 (I²C) デバイス、およびセカンダリのアダプター。

ビデオ ポート ドライバー FDO (機能のデバイス オブジェクト) を作成して受信に固有の PnP IRP のコードのディスパッチなど、ミニポート ドライバーの PnP、要件のほとんどの管理 (を参照してください[IRP の主な機能コード](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-major-function-codes)) で、ミニポート ドライバーの代わりです。

ミニポート ドライバーには、PnP をサポートするために次の関数と電源管理を実装する必要があります。

[*HwVidSetPowerState*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_power_set)

[*HwVidGetPowerState*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_power_get)

[*HwVidGetVideoChildDescriptor*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_get_child_descriptor)

システムが実行されていることもレガシ ミニポート ドライバーは実行中のシステムに追加されたときに自動的に検出中に、システムからレガシ ミニポート ドライバーのグラフィックス アダプターを削除できません。

参照してください[ディスプレイ アダプター (Windows 2000 モデル) の子デバイス](child-devices-of-the-display-adapter--windows-2000-model-.md)を検出して、アダプターの子デバイスと通信の詳細についてはします。 プラグ アンド プレイ ドライバーについては、次を参照してください。[プラグ アンド プレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)します。

 

 





