---
title: KSNODETYPE\_PROLOGIC\_エンコーダー
description: KSNODETYPE\_PROLOGIC\_エンコーダー
ms.assetid: cca6fe1d-20f8-4112-956b-a1b33b48a4ff
keywords:
- KSNODETYPE_PROLOGIC_ENCODER オーディオ デバイス
topic_type:
- apiref
api_name:
- KSNODETYPE_PROLOGIC_ENCODER
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac871e3409a14a9981c080cc33edeac6111d36e6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359011"
---
# <a name="ksnodetypeprologicencoder"></a>KSNODETYPE\_PROLOGIC\_エンコーダー


## <span id="ddk_ksnodetype_prologic_encoder_ks"></span><span id="DDK_KSNODETYPE_PROLOGIC_ENCODER_KS"></span>


KSNODETYPE\_PROLOGIC\_エンコーダーのノードがドルビー サラウンド Pro ロジック エンコーダーを表します。 ノードは、左、右、センター、およびバック スピーカーのチャネルを持つ 4 つのチャネルの入力ストリームを受け入れます。 ノードは、サラウンドでエンコードされたステレオ出力ストリームとして、入力ストリームをエンコードします。

KSNODETYPE 機能\_PROLOGIC\_エンコーダーのノードを補完するものです、 [ **KSNODETYPE\_PROLOGIC\_デコーダー** ](ksnodetype-prologic-decoder.md)ノードサラウンドでエンコードされたステレオ入力ストリームを受け取り、左、右、センター、およびバック スピーカーのチャネルを持つ 4 チャネル ストリームにデコードします。

Microsoft Windows XP 以降では、 [KMixer システム ドライバー](https://docs.microsoft.com/windows-hardware/drivers/audio/kernel-mode-wdm-audio-components#kmixer-system-driver)が、KSNODETYPE\_PROLOGIC\_エンコーダー ノード。

KSNODETYPE\_PROLOGIC\_エンコーダーのノードをサポートする必要があります、 [ **KSPROPERTY\_オーディオ\_サラウンド\_エンコード**](ksproperty-audio-surround-encode.md)プロパティこれを有効にして、ノードを無効化に使用されます。

 

 





