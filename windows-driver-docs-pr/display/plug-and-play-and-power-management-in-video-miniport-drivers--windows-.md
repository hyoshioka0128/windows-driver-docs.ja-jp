---
title: 電源管理とビデオのミニポート ドライバー (XDDM) での PnP
description: 電源管理とビデオのミニポート ドライバー (Windows 2000 モデル) のプラグ アンド プレイ
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
ms.openlocfilehash: 189c3fcf5f2fafb70244bd73bc0ffe3f1c86f9e8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529658"
---
# <a name="power-management-and-plug-and-play-in-video-miniport-drivers-windows-2000-model"></a>電源管理とビデオのミニポート ドライバー (Windows 2000 モデル) のプラグ アンド プレイ


## <span id="ddk_plug_and_play_and_power_management_in_video_miniport_drivers_windo"></span><span id="DDK_PLUG_AND_PLAY_AND_POWER_MANAGEMENT_IN_VIDEO_MINIPORT_DRIVERS_WINDO"></span>


すべての Windows 2000 およびそれ以降のミニポート ドライバーには、プラグ アンド プレイと電源管理をサポートする必要があります。 などの子デバイスを列挙する機能が含まれます*DDC*モニタ、間統合の回線 (I²C) デバイス、およびセカンダリのアダプター。

ビデオ ポート ドライバー FDO (機能のデバイス オブジェクト) を作成して受信に固有の PnP IRP のコードのディスパッチなど、ミニポート ドライバーの PnP、要件のほとんどの管理 (を参照してください[IRP の主な機能コード](https://msdn.microsoft.com/library/windows/hardware/ff550710)) で、ミニポート ドライバーの代わりです。

ミニポート ドライバーには、PnP をサポートするために次の関数と電源管理を実装する必要があります。

[*HwVidSetPowerState*](https://msdn.microsoft.com/library/windows/hardware/ff567365)

[*HwVidGetPowerState*](https://msdn.microsoft.com/library/windows/hardware/ff567336)

[*HwVidGetVideoChildDescriptor*](https://msdn.microsoft.com/library/windows/hardware/ff567341)

システムが実行されていることもレガシ ミニポート ドライバーは実行中のシステムに追加されたときに自動的に検出中に、システムからレガシ ミニポート ドライバーのグラフィックス アダプターを削除できません。

参照してください[ディスプレイ アダプター (Windows 2000 モデル) の子デバイス](child-devices-of-the-display-adapter--windows-2000-model-.md)を検出して、アダプターの子デバイスと通信の詳細についてはします。 プラグ アンド プレイ ドライバーについては、次を参照してください。[プラグ アンド プレイ](https://msdn.microsoft.com/library/windows/hardware/ff547125)します。

 

 





