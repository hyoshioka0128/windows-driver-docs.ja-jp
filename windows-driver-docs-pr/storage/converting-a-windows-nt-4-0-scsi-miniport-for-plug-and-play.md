---
title: プラグ アンド プレイの Windows NT 4.0 SCSI ミニポートに変換します。
description: プラグ アンド プレイの Windows NT 4.0 SCSI ミニポートに変換します。
ms.assetid: 46e5eb41-ff41-4054-856b-cc32f286e543
keywords:
- SCSI ミニポート ドライバー WDK 記憶域、PnP
- PnP WDK SCSI
- プラグ アンド プレイ WDK SCSI
- SCSI ミニポート ドライバーに変換します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7192f8e41bbef16bc8c0ec0d3a46fa4235327924
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548829"
---
# <a name="converting-a-windows-nt-40-scsi-miniport-for-plug-and-play"></a>プラグ アンド プレイの Windows NT 4.0 SCSI ミニポートに変換します。


## <span id="ddk_converting_a_windows_nt_4_0_scsi_miniport_for_plug_and_play_kg"></span><span id="DDK_CONVERTING_A_WINDOWS_NT_4_0_SCSI_MINIPORT_FOR_PLUG_AND_PLAY_KG"></span>


特定の制限の使用を優先しない限り、ミニポート ドライバーには、レジストリのプラグ アンド プレイが有効であって、ドライバーが初期化中にエラーは、 *HwContext*ポインターとポート ドライバーによって提供されるリソース。 ドライバーの予測可能な初期化の順序に依存している場合、ミニポート ドライバーは初期化中にエラーも可能性があります。

プラグ アンド プレイ、Microsoft Windows で正常に実行するには

NT 4.0 ミニポート ドライバーのソース コードは、次のセクションで説明したように変更する必要があります。

 

 




