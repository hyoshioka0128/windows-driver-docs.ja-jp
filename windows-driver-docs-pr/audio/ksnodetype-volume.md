---
title: KSNODETYPE\_ボリューム
description: KSNODETYPE\_ボリューム
ms.assetid: 4776ea69-6492-428e-97ce-dd8842f22c16
keywords:
- KSNODETYPE_VOLUME オーディオ デバイス
topic_type:
- apiref
api_name:
- KSNODETYPE_VOLUME
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 502b87d2ffdf8104fe17720f11920f404ebaa143
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537670"
---
# <a name="ksnodetypevolume"></a>KSNODETYPE\_ボリューム


## <span id="ddk_ksnodetype_volume_ks"></span><span id="DDK_KSNODETYPE_VOLUME_KS"></span>


KSNODETYPE\_[ボリューム] ノードはボリューム (利益または減衰) コントロールを表します。 ボリューム コントロールが 1 つの入力ストリームと 1 つの出力ストリーム。2 つのストリームは、同じデータ形式があります。 減衰 (ボリュームの削減) を適用できるまたはストリームにゲイン (ボリュームの増加)。 さらに、反転、信号をサポートできます必要に応じて。

マルチ チャネル ボリューム ノードについては、次を参照してください。[マルチ チャネルのノードを公開する](https://msdn.microsoft.com/library/windows/hardware/ff536380)します。

KSNODETYPE\_[ボリューム] ノードは、次の必要なプロパティをサポートする必要があります。

[**KSPROPERTY\_オーディオ\_VOLUMELEVEL**](ksproperty-audio-volumelevel.md)

 

 





