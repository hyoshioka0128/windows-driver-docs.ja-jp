---
title: KSEVENTSETID\_AudioControlChange
description: KSEVENTSETID\_AudioControlChange
ms.assetid: 5189c284-d53a-4fc4-981c-7d6b3851dab1
keywords:
- KSEVENTSETID_AudioControlChange
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 053b5d71edb2d567c02249a302c2a62be6d23fa9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528685"
---
# <a name="kseventsetidaudiocontrolchange"></a>KSEVENTSETID\_AudioControlChange


## <span id="ddk_kseventsetid_audiocontrolchange_ks"></span><span id="DDK_KSEVENTSETID_AUDIOCONTROLCHANGE_KS"></span>


`KSEVENTSETID_AudioControlChange`ミニポート ドライバーを検出したときにクライアントに通知するイベントのセットが使用される、[ハードウェア イベント](https://msdn.microsoft.com/library/windows/hardware/ff536405)ハードウェアのボリューム コントロール ノブ、ミュート スイッチ、または他の種類を手動で制御の変更があります。

このセット内のイベント項目が KSEVENT として指定された\_オーディオ\_コントロール\_列挙の値を変更します。

このセット内の唯一のイベントは[ **KSEVENT\_コントロール\_変更**](ksevent-control-change.md)します。

 

 





