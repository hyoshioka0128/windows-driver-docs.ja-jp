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
ms.openlocfilehash: feb4a582311c86625216a380c198a6d0915d7d75
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359007"
---
# <a name="ksnodetypevolume"></a>KSNODETYPE\_ボリューム


## <span id="ddk_ksnodetype_volume_ks"></span><span id="DDK_KSNODETYPE_VOLUME_KS"></span>


KSNODETYPE\_[ボリューム] ノードはボリューム (利益または減衰) コントロールを表します。 ボリューム コントロールが 1 つの入力ストリームと 1 つの出力ストリーム。2 つのストリームは、同じデータ形式があります。 減衰 (ボリュームの削減) を適用できるまたはストリームにゲイン (ボリュームの増加)。 さらに、反転、信号をサポートできます必要に応じて。

マルチ チャネル ボリューム ノードについては、次を参照してください。[マルチ チャネルのノードを公開する](https://docs.microsoft.com/windows-hardware/drivers/audio/exposing-multichannel-nodes)します。

KSNODETYPE\_[ボリューム] ノードは、次の必要なプロパティをサポートする必要があります。

[**KSPROPERTY\_オーディオ\_VOLUMELEVEL**](ksproperty-audio-volumelevel.md)

 

 





