---
title: SCSI ミニポート ドライバーでのプラグ アンド プレイのサポート
description: SCSI ミニポート ドライバーでのプラグ アンド プレイのサポート
ms.assetid: c8b148ac-b1ab-4870-8818-5ef1c2d68599
keywords:
- SCSI ミニポート ドライバー WDK 記憶域、PnP
- PnP WDK SCSI
- プラグ アンド プレイ WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 982e5f875ec298c8c6b2bd1ff0426ee456ba0dc1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578482"
---
# <a name="supporting-plug-and-play-in-a-scsi-miniport-driver"></a>SCSI ミニポート ドライバーでのプラグ アンド プレイのサポート


## <span id="ddk_supporting_plug_and_play_in_a_scsi_miniport_driver_kg"></span><span id="DDK_SUPPORTING_PLUG_AND_PLAY_IN_A_SCSI_MINIPORT_DRIVER_KG"></span>


Microsoft Windows 2000 と以降のオペレーティング システムは、プラグ アンド プレイのオペレーティング システムには、既定では SCSI ミニポート ドライバーは従来のドライバーとして実行されます。 実行されているとは従来のミニポート ドライバーが実行中のシステムに追加されたときに自動的に検出中に、システムからレガシ ミニポート ドライバーに HBA を削除できません。 これらの制限は、特定の Hba のもかまいませんが、ラップトップ PC カードまたは CardBus Hba、Hba の SCSI ミニポート ドライバーがプラグ アンド プレイをサポートする必要があります。

プラグ アンド プレイのミニポート ドライバーを実装する必要があります、 *HwScsiAdapterControl*ルーチンを停止し、HBA に電源を管理します。 ルーチンを追加するドライバーの初期化の変化に合わせて、プラグ アンド プレイのミニポート ドライバーの必要はありません。

SCSI ポート ドライバーでは、追加、開始またはミニポート ドライバーに代わって、デバイスをアンロードするには、ターゲット デバイスの Pdo とミニポート ドライバー、および要求を処理 FDO を作成します。 プラグ アンド プレイ ドライバーについては、[プラグ アンド プレイ](https://msdn.microsoft.com/library/windows/hardware/ff547125)を参照してください。

 

 




