---
title: KSNODETYPE\_PEAKMETER
description: KSNODETYPE\_PEAKMETER
ms.assetid: 11c886eb-dd63-44dd-9bca-dd19a8dd6948
keywords:
- KSNODETYPE_PEAKMETER オーディオ デバイス
topic_type:
- apiref
api_name:
- KSNODETYPE_PEAKMETER
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a49e0580d4525ec9aef7d98f9da4cbac45ab470
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359023"
---
# <a name="ksnodetypepeakmeter"></a>KSNODETYPE\_PEAKMETER


## <span id="ddk_ksnodetype_peakmeter_ks"></span><span id="DDK_KSNODETYPE_PEAKMETER_KS"></span>


KSNODETYPE\_PEAKMETER ノードは、ハードウェア peakmeter を表します。 KS peakmeter ノードが 1 つの入力ピンと 1 つの出力ピン、2 つの pin が同じデータ形式を共有します。

KS peakmeter は、前回、peakmeter はゼロにリセットされた後、オーディオ信号の最大値を内部的に記録します。 Peakmeter、自動的にそれ自体を 0 にリセット IOCTL 後\_KS\_プロパティの取得要求を[ **KSPROPERTY\_オーディオ\_PEAKMETER** ](ksproperty-audio-peakmeter.md)プロパティ。

Peakmeter には、ハードウェアのサポートが必要です。 ソフトウェア peakmeter は現実的ではないと、これは、アダプターのドライバーでは、行で、マイク、または再生チャネルとが混在するその他の入力の上に存在する信号にアクセスできないためです。

Peakmeter ノードに、ストリームは、フィルター内で渡されます。 最後のノードを作成することをお勧めします。 レンダリング ストリームにオーディオのアダプターの通常の接続 peakmeter ノード マスター出力後[ **KSNODETYPE\_ミュート**](ksnodetype-mute.md)ノードまたは[ **KSNODETYPE\_ボリューム**](ksnodetype-volume.md)ノード。 同じアプローチは、キャプチャ ストリームまたは peakmeter ノードは、フィルターが組み込まれています. その他の任意のストリームに適用されます。

オーディオのアダプターの名前 peakmeter ノード KSAUDFNAME\_PEAKMETER します。

Peakmeter ノードは、プロパティのフラグのプロパティ ハンドラーを用意する必要があります (を参照してください[ **KSPROPERTY**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)))、次の表に表示されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">フラグ名</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>KSPROPERTY_TYPE_GET</p></td>
<td align="left"><p>ハードウェア peakmeter の現在の値を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSPROPERTY_TYPE_BASICSUPPORT</p></td>
<td align="left"><p>16 ビットのデジタル オーディオのデータの範囲である 32767 の間、-32768 からのデータ範囲を返します。</p></td>
</tr>
</tbody>
</table>

 

プロパティ ハンドラーの入力パラメーターを確認する必要があり、左へ、チャネル情報を右します。

Peakmeter ノードでは、次の表に、プロパティもサポートする必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">プロパティ名</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="ksproperty-audio-peakmeter.md" data-raw-source="[&lt;strong&gt;KSPROPERTY_AUDIO_PEAKMETER&lt;/strong&gt;](ksproperty-audio-peakmeter.md)"><strong>KSPROPERTY_AUDIO_PEAKMETER</strong></a></p></td>
<td align="left"><p>Peakmeter コントロールを表します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ksproperty-audio-cpu-resources.md" data-raw-source="[&lt;strong&gt;KSPROPERTY_AUDIO_CPU_RESOURCES&lt;/strong&gt;](ksproperty-audio-cpu-resources.md)"><strong>KSPROPERTY_AUDIO_CPU_RESOURCES</strong></a></p></td>
<td align="left"><p>指定したノードの機能では、ホストの CPU の使用によってかどうかを示します。</p></td>
</tr>
</tbody>
</table>

 

 

 





