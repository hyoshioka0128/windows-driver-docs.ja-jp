---
title: KSNODETYPE\_音響\_エコー\_キャンセル
description: KSNODETYPE\_音響\_エコー\_キャンセル
ms.assetid: 5f70b9ad-d569-404a-bf6d-01be689e2d56
keywords:
- KSNODETYPE_ACOUSTIC_ECHO_CANCEL Audio Devices
topic_type:
- apiref
api_name:
- KSNODETYPE_ACOUSTIC_ECHO_CANCEL
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3f4986473e7b3a335072957f839d36ec25c4614
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360643"
---
# <a name="ksnodetypeacousticechocancel"></a>KSNODETYPE\_音響\_エコー\_キャンセル


## <span id="ddk_ksnodetype_acoustic_echo_cancel_ks"></span><span id="DDK_KSNODETYPE_ACOUSTIC_ECHO_CANCEL_KS"></span>


KSNODETYPE\_音響\_エコー\_キャンセル ノードは、AEC (アコースティック エコー キャンセル) コントロールを表します。 AEC にノードが 2 つの入力ストリームの接続と、2 つの出力ストリーム。 1 つの入力/出力のペアは、キャプチャしたストリーム用使用され、レンダリング ストリームの他の入力/出力のペアが使用されます。 キャプチャ出力およびレンダリング入力ストリームと同じ形式であります。 キャプチャ入力とレンダリング出力ストリームには、チャネルと異なるサンプル レートの数が異なることができます。 ただし、一般的な実装で 2 つのストリームがあるか、同じサンプル速度または 16 kHz と 48 kHz または 11.025 kHz 44.1 kHz、どの 1 つのサンプル レートは整数などの組み合わせをもう一方の倍数です。

AEC のノードをその論理ピンが次の表に示されているヘッダー ファイル、Ksmedia.h からピン留めする Id 番号を付けます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">暗証番号 (pin) の ID パラメーター</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>KSNODEPIN_AEC_RENDER_IN</p></td>
<td align="left"><p>レンダリングのストリームのシンクのピン (ノードの入力)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODEPIN_AEC_RENDER_OUT</p></td>
<td align="left"><p>ストリームのソース pin (ノードの出力) を描画します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODEPIN_AEC_CAPTURE_IN</p></td>
<td align="left"><p>シンクのキャプチャのストリームの pin (ノードの入力)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODEPIN_AEC_CAPTURE_OUT</p></td>
<td align="left"><p>キャプチャのストリームのソースの pin (ノードの出力)。</p></td>
</tr>
</tbody>
</table>

 

上記の表のピンが、フィルターでは、他のフィルターへの接続に使用される外部のピンではなく、ノードで、フィルターに内部の接続を指定するためだけに使用される、論理ピンことに注意してください。 詳細については、次を参照してください。 [ **PCCONNECTION\_記述子**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537688(v=vs.85))します。

AEC のノードを含むフィルターが全二重 DirectSound アプリケーションのサポートを提供する方法については、次を参照してください。 [DirectSound キャプチャ効果](https://docs.microsoft.com/windows-hardware/drivers/audio/directsound-capture-effects)します。

AEC のノードを格納しているフィルターが作成されるか、ノードがリセットされた、ときに、ノードがパススルー モードで動作する初期構成されます。

KSNODETYPE\_音響\_エコー\_キャンセル ノードは、ハードウェア アクセラレータを有効にするには、次のプロパティをサポートする必要があります。

[**KSPROPERTY\_AUDIO\_CPU\_RESOURCES**](ksproperty-audio-cpu-resources.md)

[**KSPROPERTY\_オーディオ\_アルゴリズム\_インスタンス**](ksproperty-audio-algorithm-instance.md)

[**KSPROPERTY\_TOPOLOGYNODE\_を有効にします。** ](ksproperty-topologynode-enable.md)

[**KSPROPERTY\_TOPOLOGYNODE\_リセット**](ksproperty-topologynode-reset.md)

KSPROPERTY\_TOPOLOGYNODE\_を有効にして、AEC のノードを無効化を有効にするプロパティを使用します。 無効の場合、ノードはパススルー モードで動作します。つまり、変更しなくても、ノードを通過するレンダリングおよびキャプチャのストリームができます。

KSNODETYPE\_音響\_エコー\_[キャンセル] ノードでは、次の省略可能なプロパティの詳細に制御および監視機能を提供するためにもサポートできます。

[**KSPROPERTY\_AEC\_モード**](ksproperty-aec-mode.md)

[**KSPROPERTY\_AEC\_ノイズ\_入力\_を有効にします。** ](ksproperty-aec-noise-fill-enable.md)

[**KSPROPERTY\_AEC\_状態**](ksproperty-aec-status.md)

 

 





