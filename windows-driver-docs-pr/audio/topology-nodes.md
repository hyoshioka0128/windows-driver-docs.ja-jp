---
title: トポロジのノード
description: トポロジのノード
ms.assetid: 39827413-2b6b-4925-97bb-e0f3e3428b13
keywords:
- トポロジ ノードの WDK オーディオ
- WDK オーディオ、トポロジのノード
- MIXERCONTROL 構造体
- トーン ノード WDK オーディオ
- 変換ノード WDK オーディオ
- supermix ノード WDK オーディオ
- 低音プロパティ WDK オーディオ
- 高音の WDK オーディオのプロパティ
- 低音ブースト WDK オーディオのプロパティ
- 中間の頻度 プロパティの WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1aa4195e0b0c55b1945e5b08cf161e71e69da36d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328546"
---
# <a name="topology-nodes"></a>トポロジのノード


## <span id="topology_nodes"></span><span id="TOPOLOGY_NODES"></span>


オーディオ アプリケーションは、Microsoft Windows のマルチ メディア機能ミキサーの制御をアクセスできる[ **mixerGetLineControls**](https://msdn.microsoft.com/library/windows/desktop/dd757302)します。 この関数は、オーディオの行に 状態と 1 つのコントロールのノードのメトリックについて説明しますそれぞれが 1 つまたは複数の MIXERCONTROL 構造体の配列を取得します。 **DwControlType** MIXERCONTROL 構造体のメンバーは、コントロールの種類を指定する列挙値に設定します。 オーディオの Vxd ミキサー コントロールの種類の数値が指定されているが、これらのコントロールのサブセットのみが WDM オーディオ ドライバーの使用可能です。

WDMAud では、いくつかのトポロジ ノードを対応するミキサー行コントロールに変換します。 次の表に記載されているトポロジ ノードの種類があるミキサー ライン コントロールである対応します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ノードの種類</th>
<th align="left">トポロジ ノードの種類名</th>
<th align="left">Mixer コントロールの種類名</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>AGC</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537154" data-raw-source="[&lt;strong&gt;KSNODETYPE_AGC&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537154)"><strong>KSNODETYPE_AGC</strong></a></p></td>
<td align="left"><p>MIXERCONTROL_CONTROLTYPE_ONOFF</p></td>
</tr>
<tr class="even">
<td align="left"><p>ラウドネス</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537174" data-raw-source="[&lt;strong&gt;KSNODETYPE_LOUDNESS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537174)"><strong>KSNODETYPE_LOUDNESS</strong></a></p></td>
<td align="left"><p>MIXERCONTROL_CONTROLTYPE_LOUDNESS</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Mute</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537178" data-raw-source="[&lt;strong&gt;KSNODETYPE_MUTE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537178)"><strong>KSNODETYPE_MUTE</strong></a></p></td>
<td align="left"><p>MIXERCONTROL_CONTROLTYPE_MUTE</p></td>
</tr>
<tr class="even">
<td align="left"><p>トーン (複数)</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537205" data-raw-source="[&lt;strong&gt;KSNODETYPE_TONE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537205)"><strong>KSNODETYPE_TONE</strong></a></p></td>
<td align="left"><p>MIXERCONTROL_CONTROLTYPE_ONOFF (KSPROPERTY_AUDIO_BASS_BOOST がサポートされている) 場合</p>
<p>MIXERCONTROL_CONTROLTYPE_BASS (KSPROPERTY_AUDIO_BASS がサポートされている) 場合</p>
<p>MIXERCONTROL_CONTROLTYPE_TREBLE (KSPROPERTY_AUDIO_TREBLE がサポートされている) 場合</p></td>
</tr>
<tr class="odd">
<td align="left"><p>[ボリューム]</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537208" data-raw-source="[&lt;strong&gt;KSNODETYPE_VOLUME&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537208)"><strong>KSNODETYPE_VOLUME</strong></a></p></td>
<td align="left"><p>MIXERCONTROL_CONTROLTYPE_VOLUME</p></td>
</tr>
<tr class="even">
<td align="left"><p>Peakmeter</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537183" data-raw-source="[&lt;strong&gt;KSNODETYPE_PEAKMETER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537183)"><strong>KSNODETYPE_PEAKMETER</strong></a></p></td>
<td align="left"><p>MIXERCONTROL_CONTROLTYPE_PEAKMETER</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MUX</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537180" data-raw-source="[&lt;strong&gt;KSNODETYPE_MUX&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537180)"><strong>KSNODETYPE_MUX</strong></a></p></td>
<td align="left"><p>MIXERCONTROL_CONTROLTYPE_MUX</p></td>
</tr>
<tr class="even">
<td align="left"><p>ワイド ステレオ</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537194" data-raw-source="[&lt;strong&gt;KSNODETYPE_STEREO_WIDE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537194)"><strong>KSNODETYPE_STEREO_WIDE</strong></a></p></td>
<td align="left"><p>MIXERCONTROL_CONTROLTYPE_FADER</p></td>
</tr>
<tr class="odd">
<td align="left"><p>コーラス</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537156" data-raw-source="[&lt;strong&gt;KSNODETYPE_CHORUS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537156)"><strong>KSNODETYPE_CHORUS</strong></a></p></td>
<td align="left"><p>MIXERCONTROL_CONTROLTYPE_FADER</p></td>
</tr>
<tr class="even">
<td align="left"><p>リバーブ</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537189" data-raw-source="[&lt;strong&gt;KSNODETYPE_REVERB&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537189)"><strong>KSNODETYPE_REVERB</strong></a></p></td>
<td align="left"><p>MIXERCONTROL_CONTROLTYPE_FADER</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Supermix (複数)</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537198" data-raw-source="[&lt;strong&gt;KSNODETYPE_SUPERMIX&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537198)"><strong>KSNODETYPE_SUPERMIX</strong></a></p></td>
<td align="left"><p>MIXERCONTROL_CONTROLTYPE_MUTE (KSPROPERTY_AUDIO_MUTE は supermix ノードでサポートされている) 場合</p>
<p>MIXERCONTROL_CONTROLTYPE_VOLUME (テキスト コメントを参照してください)</p></td>
</tr>
</tbody>
</table>

 

上記の表の不足しているトポロジ ノードの種類はミキサー行コントロールに翻訳されないと WDM オーディオ ドライバーでは、テーブルから欠落しているミキサー行コントロールはサポートされていません。

注その MIXERCONTROL\_CONTROLTYPE\_カスタムがテーブルにありません。 これは WDM オーディオ ドライバーは、カスタム ミキサーの制御をサポートされていないことを意味します。

A [**トーン ノード**](https://msdn.microsoft.com/library/windows/hardware/ff537205) 4 つのプロパティをサポートしています: [**低音**](https://msdn.microsoft.com/library/windows/hardware/ff537242)、 [**高音**](https://msdn.microsoft.com/library/windows/hardware/ff537308)、 [**中間頻度**](https://msdn.microsoft.com/library/windows/hardware/ff537290)、および[**低音ブースト**](https://msdn.microsoft.com/library/windows/hardware/ff537245)します。 中間頻度プロパティには、ミキサー行の対応がありませんが、その他の 3 つのプロパティの操作を行います。 トポロジで検出された各トーン ノードは、クエリはサポートされているプロパティのそれぞれに対して行われました。

[**KSPROPERTY\_オーディオ\_低音**](https://msdn.microsoft.com/library/windows/hardware/ff537242)

[**KSPROPERTY\_AUDIO\_TREBLE**](https://msdn.microsoft.com/library/windows/hardware/ff537308)

[**KSPROPERTY\_オーディオ\_低音\_BOOST**](https://msdn.microsoft.com/library/windows/hardware/ff537245)

各プロパティのクエリが成功するには、ミキサー行コントロールが生成されます。 名前付けの問題では、トーンの 1 つのノードが 1 つのプロパティのみをサポートする必要があります。 デバイスは、低音と高音の両方をサポートする場合などが必要トーンの 2 つのノード、ノードが異なる名前を付けることができるようにします。

A [ **supermix ノード**](https://msdn.microsoft.com/library/windows/hardware/ff537198)最大 2 つのコントロールをサポートしています: ミュートやボリューム。 Supermix ノードは supermix ノードのすべてのエントリの 1 つ以上のこれらの 2 つの条件を満たす場合、ミュート用のコントロールとして使用できます[**機能テーブル**](https://msdn.microsoft.com/library/windows/hardware/ff537088):

-   エントリで指定したとおり、ミュートのプロパティがサポートされている、**機能**.**ミュート**フラグ。

-   エントリが完全に減衰 (-無限大デシベル単位減衰) の両方で指定されるにことはできませんと**機能**.**最小**と**機能**.**最大**時間の長い値を持つ\_MIN (0x80000000)。

Supermix ノードは、supermix 機能の表に、すべてのエントリがある 0 以外の値の範囲と、ボリューム コントロールとして使用できます。 その他のすべてのコントロールは、一対一で変換されます。 認識されているノードが検出されたときに、ミキサー行ドライバーは、そのノードのそれぞれのプロパティを照会します。

右のチャンネルでは、後に、左側のチャネルが照会されたステレオや mono のサポートを確認して、最後に、これらの両方が失敗した場合、マスターのチャネル (-1) が試行されます。 これらのクエリのいずれも成功すると、そのノードのコントロールは生成されません。 MUX ノードが各チャネルに対して照会しないことに注意してください。 代わりに、MUX の現在の選択範囲を取得する 1 つのクエリを実行します。

ノードがクエリされるときに、コントロールの名前は文字列として返されますその[ **KSPROPERTY\_トポロジ\_名前**](https://msdn.microsoft.com/library/windows/hardware/ff565809)プロパティ。 ノードは、1 つ以上のコントロールを生成する場合、すべてのコントロールは、同じ名前を共有します。

 

 




