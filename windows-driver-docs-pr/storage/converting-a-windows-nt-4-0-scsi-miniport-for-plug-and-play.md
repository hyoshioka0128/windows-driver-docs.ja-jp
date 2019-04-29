---
title: Windows NT 4.0 SCSI ミニポートをプラグ アンド プレイ対応にするための変換
description: Windows NT 4.0 SCSI ミニポートをプラグ アンド プレイ対応にするための変換
ms.assetid: 46e5eb41-ff41-4054-856b-cc32f286e543
keywords:
- SCSI ミニポート ドライバー WDK 記憶域、PnP
- PnP WDK SCSI
- プラグ アンド プレイ WDK SCSI
- SCSI ミニポート ドライバーに変換します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7192f8e41bbef16bc8c0ec0d3a46fa4235327924
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330451"
---
# <a name="converting-a-windows-nt-40-scsi-miniport-for-plug-and-play"></a>Windows NT 4.0 SCSI ミニポートをプラグ アンド プレイ対応にするための変換


## <span id="ddk_converting_a_windows_nt_4_0_scsi_miniport_for_plug_and_play_kg"></span><span id="DDK_CONVERTING_A_WINDOWS_NT_4_0_SCSI_MINIPORT_FOR_PLUG_AND_PLAY_KG"></span>


特定の制限の使用を優先しない限り、ミニポート ドライバーには、レジストリのプラグ アンド プレイが有効であって、ドライバーが初期化中にエラーは、 *HwContext*ポインターとポート ドライバーによって提供されるリソース。 ドライバーの予測可能な初期化の順序に依存している場合、ミニポート ドライバーは初期化中にエラーも可能性があります。

プラグ アンド プレイ、Microsoft Windows で正常に実行するには

NT 4.0 ミニポート ドライバーのソース コードは、次のセクションで説明したように変更する必要があります。

 

 




