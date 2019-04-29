---
title: プラグ アンド プレイの SCSI ミニポートで提供されたリソースのみの使用
description: プラグ アンド プレイの SCSI ミニポートで提供されたリソースのみの使用
ms.assetid: 26c688dc-b6af-4a0c-8401-d53e653d90b3
keywords:
- SCSI ミニポート ドライバー WDK 記憶域、PnP
- PnP WDK SCSI
- プラグ アンド プレイ WDK SCSI
- SCSI ミニポート ドライバーに変換します。
- リソース制限 WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ec21cad95e73fee1f7e0d2d47b354bbdd9cf135
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339841"
---
# <a name="use-only-supplied-resources-in-a-plug-and-play-scsi-miniport"></a>プラグ アンド プレイの SCSI ミニポートで提供されたリソースのみの使用


## <span id="ddk_use_only_supplied_resources_in_a_plug_and_play_scsi_miniport_kg"></span><span id="DDK_USE_ONLY_SUPPLIED_RESOURCES_IN_A_PLUG_AND_PLAY_SCSI_MINIPORT_KG"></span>


削減または排除、いくつかの既知のメモリの場所にアクセスして自分のデバイスを検出するドライバーのプラグ アンド プレイ システムの目標の 1 つです。 これには、その HBA の構成領域を読み取ることによって、リソースを決定するドライバーが含まれます。

プラグ アンド プレイでは、列挙可能なバス上のデバイスは、バス ドライバーによって検出されます。 特殊なケースの修正プログラムを提供すると、破損したバスとブリッジのパーツなどのこれにより、リソースの競合を処理するために、バス ドライバー。

その結果、SCSI ミニポート ドライバーでは、Microsoft Windows 2000 以降のシステムで、ポート ドライバー (ある場合) によって提供されるリソースのみを使用する必要があります。 ミニポート ドライバーが許可されたポート ドライバーが値 0 のアクセスの範囲で渡す場合にのみ、HBA のバスをスキャンします。 ミニポート ドライバーは、それに割り当てられていないリソースを使用しようとすると、 [ **ScsiPortGetDeviceBase** ](https://msdn.microsoft.com/library/windows/hardware/ff564629)呼び出しは失敗します。 通話の読み取りし、書き込みのデバイスを登録または正しくマップされていないポートも失敗する可能性があります。

 

 




