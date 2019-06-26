---
title: KSEVENTSETID\_AudioControlChange
description: KSEVENTSETID\_AudioControlChange
ms.assetid: 5189c284-d53a-4fc4-981c-7d6b3851dab1
keywords:
- KSEVENTSETID_AudioControlChange
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c71db9e668db4dff29a62b63101ec5845c148a0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359795"
---
# <a name="kseventsetidaudiocontrolchange"></a>KSEVENTSETID\_AudioControlChange


## <span id="ddk_kseventsetid_audiocontrolchange_ks"></span><span id="DDK_KSEVENTSETID_AUDIOCONTROLCHANGE_KS"></span>


`KSEVENTSETID_AudioControlChange`ミニポート ドライバーを検出したときにクライアントに通知するイベントのセットが使用される、[ハードウェア イベント](https://docs.microsoft.com/windows-hardware/drivers/audio/hardware-events)ハードウェアのボリューム コントロール ノブ、ミュート スイッチ、または他の種類を手動で制御の変更があります。

このセット内のイベント項目が KSEVENT として指定された\_オーディオ\_コントロール\_列挙の値を変更します。

このセット内の唯一のイベントは[ **KSEVENT\_コントロール\_変更**](ksevent-control-change.md)します。

 

 





