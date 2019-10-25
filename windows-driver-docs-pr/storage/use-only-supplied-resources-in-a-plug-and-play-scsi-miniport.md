---
title: プラグ アンド プレイの SCSI ミニポートで提供されたリソースのみの使用
description: プラグ アンド プレイの SCSI ミニポートで提供されたリソースのみの使用
ms.assetid: 26c688dc-b6af-4a0c-8401-d53e653d90b3
keywords:
- SCSI ミニポートドライバー WDK 記憶域、PnP
- PnP WDK SCSI
- WDK SCSI のプラグアンドプレイ
- SCSI ミニポートドライバーの変換
- リソース制限 WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f8da9555242ef358b7b8fb161a0b95f34d239bf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845443"
---
# <a name="use-only-supplied-resources-in-a-plug-and-play-scsi-miniport"></a>プラグ アンド プレイの SCSI ミニポートで提供されたリソースのみの使用


## <span id="ddk_use_only_supplied_resources_in_a_plug_and_play_scsi_miniport_kg"></span><span id="DDK_USE_ONLY_SUPPLIED_RESOURCES_IN_A_PLUG_AND_PLAY_SCSI_MINIPORT_KG"></span>


プラグアンドプレイシステムの目標の1つは、既知のメモリの場所にアクセスすることによってデバイスを検出するドライバーの数を減らしたり、削除したりすることです。 これには、HBA の構成領域を読み取ることによってリソースを決定するドライバーが含まれます。

プラグアンドプレイでは、バスのドライバーによって、列挙可能なバス上のデバイスが検出されます。 これにより、バスドライバーはリソースの競合を処理し、障害が発生したバスやブリッジパーツに対して特殊なケース修正を行うことができます。

そのため、SCSI ミニポートドライバーは、Microsoft Windows 2000 以降のシステムで、ポートドライバーによって提供されるリソース (存在する場合) のみを使用する必要があります。 ポートドライバーがゼロ値のアクセス範囲を通過した場合にのみ、ミニポートドライバーで HBA のバスをスキャンできます。 ミニポートドライバーが割り当てられていないリソースを使用しようとすると、 [**ScsiPortGetDeviceBase**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportgetdevicebase)の呼び出しは失敗します。 また、正常にマップされていないデバイスレジスタまたはポートの読み取りと書き込みの呼び出しも失敗する可能性があります。

 

 




