---
title: KSNODETYPE\_PROLOGIC\_デコーダー
description: KSNODETYPE\_PROLOGIC\_デコーダー
ms.assetid: 905ff503-1aff-4490-bd6f-f6bec8e7c3d6
keywords:
- KSNODETYPE_PROLOGIC_DECODER オーディオ デバイス
topic_type:
- apiref
api_name:
- KSNODETYPE_PROLOGIC_DECODER
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d1cdc6aeb7e0627fea33da6e160b49b75c596c5c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333199"
---
# <a name="ksnodetypeprologicdecoder"></a>KSNODETYPE\_PROLOGIC\_デコーダー


## <span id="ddk_ksnodetype_prologic_decoder_ks"></span><span id="DDK_KSNODETYPE_PROLOGIC_DECODER_KS"></span>


KSNODETYPE\_PROLOGIC\_デコーダーのノードがドルビー サラウンド Pro ロジック デコーダーを表します。 デコーダーのコントロールには、1 つのステレオ入力ストリームと 1 ~ 4 個のチャネルで 1 つの出力ストリームがあります。 4-チャネルの出力の形式で、チャネルは、左、右、センター、およびバックのスピーカーにマップされます。 3 つのチャネルの出力の形式では、チャネルは、左、右にマップされ、スピーカーをバックアップします。

KSNODETYPE 機能\_PROLOGIC\_デコーダーのノードを補完するものです、 [ **KSNODETYPE\_PROLOGIC\_エンコーダー** ](ksnodetype-prologic-encoder.md)ノードこれには、サラウンドでエンコードされたステレオ出力ストリームに 4 つのチャネルの入力ストリームに変換します。

KSNODETYPE\_PROLOGIC\_デコーダー ノードは、次の必須プロパティをサポートする必要があります。

[**KSPROPERTY\_オーディオ\_チャネル\_構成**](ksproperty-audio-channel-config.md)

[**KSPROPERTY\_TOPOLOGYNODE\_を有効にします。**](ksproperty-topologynode-enable.md)

[**KSPROPERTY\_TOPOLOGYNODE\_リセット**](ksproperty-topologynode-reset.md)

KSPROPERTY\_オーディオ\_チャネル\_構成プロパティを設定およびノードの出力ストリームのチャネルの構成を取得します。

 

 





