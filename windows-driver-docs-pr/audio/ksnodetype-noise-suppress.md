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
ms.openlocfilehash: e8b1afb48f7169a382a30282d61c17f4dc6cc26c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556716"
---
# <a name="ksnodetypenoisesuppress"></a>KSNODETYPE\_ノイズ\_を抑制します。


## <span id="ddk_ksnodetype_noise_suppress_ks"></span><span id="DDK_KSNODETYPE_NOISE_SUPPRESS_KS"></span>


KSNODETYPE\_ノイズ\_を抑制するノードは、ノイズの抑制 (NS) コントロールを表します。 NS ノードには、1 つの入力ストリームと 1 つの出力ストリームの接続があります。 両方のストリームと同じ形式であります。

NS ノードを格納しているフィルターが作成されるか、ノードがリセットされた、ときに、ノードがパススルー モードで動作する初期構成されます。

NS ノードは、全二重 DirectSound アプリケーションをサポートするために、AEC (アコースティック エコー キャンセル) フィルターに組み込むことができます。 詳細については、次を参照してください。 [DirectSound キャプチャ効果](https://msdn.microsoft.com/library/windows/hardware/ff536327)します。

KSNODETYPE\_ノイズ\_AEC フィルター ノードを抑制するハードウェア アクセラレータを有効にするには、次のプロパティをサポートする必要があります。

[**KSPROPERTY\_AUDIO\_CPU\_RESOURCES**](ksproperty-audio-cpu-resources.md)

[**KSPROPERTY\_オーディオ\_アルゴリズム\_インスタンス**](ksproperty-audio-algorithm-instance.md)

[**KSPROPERTY\_TOPOLOGYNODE\_を有効にします。**](ksproperty-topologynode-enable.md)

[**KSPROPERTY\_TOPOLOGYNODE\_リセット**](ksproperty-topologynode-reset.md)

KSPROPERTY\_TOPOLOGYNODE\_両方を有効にして、ノードを無効に有効にするプロパティを使用します。 ノードはパススルー モードで動作を無効にした場合 (変更なしの出力に渡す入力ストリームを許可、)。

 

 





