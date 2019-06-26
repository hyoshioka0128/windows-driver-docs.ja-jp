---
title: KSNODETYPE\_ノイズ\_を抑制します。
description: KSNODETYPE\_ノイズ\_を抑制します。
ms.assetid: 416504e2-38eb-4cfd-ae20-6f1f44a82abd
keywords:
- KSNODETYPE_NOISE_SUPPRESS オーディオ デバイス
topic_type:
- apiref
api_name:
- KSNODETYPE_NOISE_SUPPRESS
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e8ab8c7a3ab1eb4358c9f70d5d53fef6bef4e75
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359019"
---
# <a name="ksnodetypenoisesuppress"></a>KSNODETYPE\_ノイズ\_を抑制します。


## <span id="ddk_ksnodetype_noise_suppress_ks"></span><span id="DDK_KSNODETYPE_NOISE_SUPPRESS_KS"></span>


KSNODETYPE\_ノイズ\_を抑制するノードは、ノイズの抑制 (NS) コントロールを表します。 NS ノードには、1 つの入力ストリームと 1 つの出力ストリームの接続があります。 両方のストリームと同じ形式であります。

NS ノードを格納しているフィルターが作成されるか、ノードがリセットされた、ときに、ノードがパススルー モードで動作する初期構成されます。

NS ノードは、全二重 DirectSound アプリケーションをサポートするために、AEC (アコースティック エコー キャンセル) フィルターに組み込むことができます。 詳細については、次を参照してください。 [DirectSound キャプチャ効果](https://docs.microsoft.com/windows-hardware/drivers/audio/directsound-capture-effects)します。

KSNODETYPE\_ノイズ\_AEC フィルター ノードを抑制するハードウェア アクセラレータを有効にするには、次のプロパティをサポートする必要があります。

[**KSPROPERTY\_AUDIO\_CPU\_RESOURCES**](ksproperty-audio-cpu-resources.md)

[**KSPROPERTY\_オーディオ\_アルゴリズム\_インスタンス**](ksproperty-audio-algorithm-instance.md)

[**KSPROPERTY\_TOPOLOGYNODE\_を有効にします。** ](ksproperty-topologynode-enable.md)

[**KSPROPERTY\_TOPOLOGYNODE\_リセット**](ksproperty-topologynode-reset.md)

KSPROPERTY\_TOPOLOGYNODE\_両方を有効にして、ノードを無効に有効にするプロパティを使用します。 ノードはパススルー モードで動作を無効にした場合 (変更なしの出力に渡す入力ストリームを許可、)。

 

 





