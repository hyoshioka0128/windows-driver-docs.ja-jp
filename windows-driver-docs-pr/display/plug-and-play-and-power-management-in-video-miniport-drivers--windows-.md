---
title: ビデオミニポートドライバー (XDDM) の電源管理と PnP
description: ビデオ ミニポート ドライバーでの電源管理およびプラグ アンド プレイ (Windows 2000 モデル)
ms.assetid: e5b2ac53-e492-43de-91a3-5b02c26ee9a3
keywords:
- ビデオミニポートドライバー WDK Windows 2000、プラグアンドプレイ
- ビデオミニポートドライバー WDK Windows 2000、電源管理
- WDK ビデオミニポートのプラグアンドプレイ
- PnP WDK ビデオミニポート
- 電源管理 WDK ビデオミニポート
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 245bbfbc216941fe009476bea7bef558b21fefb6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829785"
---
# <a name="power-management-and-plug-and-play-in-video-miniport-drivers-windows-2000-model"></a>ビデオ ミニポート ドライバーでの電源管理およびプラグ アンド プレイ (Windows 2000 モデル)


## <span id="ddk_plug_and_play_and_power_management_in_video_miniport_drivers_windo"></span><span id="DDK_PLUG_AND_PLAY_AND_POWER_MANAGEMENT_IN_VIDEO_MINIPORT_DRIVERS_WINDO"></span>


すべての Windows 2000 およびそれ以降のミニポートドライバーは、プラグアンドプレイと電源管理をサポートしている必要があります。 これには、 *DDC*モニター、クロス統合回線 (I ² C) デバイス、セカンダリアダプターなどの子デバイスを列挙する機能が含まれます。

ビデオポートドライバーは、ミニポートドライバーのほとんどの PnP 要件を管理します。たとえば、FDO (機能デバイスオブジェクト) を作成し、PnP 固有の IRP コードを受信およびディスパッチします (「 [IRP Major Function コード](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-major-function-codes)」を参照してください).

ミニポートドライバーは、PnP と電源管理をサポートするために次の機能を実装する必要があります。

[*HwVidSetPowerState*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_power_set)

[*HwVidGetPowerState*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_power_get)

[*HwVidGetVideoChildDescriptor*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_get_child_descriptor)

システムの実行中に、レガシミニポートドライバーのグラフィックスアダプターをシステムから削除することはできません。また、実行中のシステムに追加したときに、レガシミニポートドライバーが自動的に検出されることもありません。

アダプターの子デバイスの検出と通信の詳細については[、「ディスプレイアダプターの子デバイス (Windows 2000 モデル)](child-devices-of-the-display-adapter--windows-2000-model-.md) 」を参照してください。 プラグアンドプレイドライバーに関する一般的な情報については、「[プラグアンドプレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)」を参照してください。

 

 





