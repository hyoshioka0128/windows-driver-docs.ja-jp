---
title: トポロジのノード
description: トポロジのノード
ms.assetid: 39827413-2b6b-4925-97bb-e0f3e3428b13
keywords:
- トポロジノード WDK オーディオ
- ノード WDK オーディオ、トポロジ
- MIXERCONTROL 構造体
- 声調ノード WDK オーディオ
- ノードの変換 (WDK オーディオ)
- ノードのスーパーミックス WDK オーディオ
- 低音プロパティ WDK オーディオ
- 高音プロパティ WDK audio
- 低音ブーストプロパティ WDK audio
- mid frequency プロパティ WDK audio
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ffd75cd453016ebc9ad75ba8334f5b6801d09b7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829997"
---
# <a name="topology-nodes"></a>トポロジのノード


## <span id="topology_nodes"></span><span id="TOPOLOGY_NODES"></span>


オーディオアプリケーションは、Microsoft Windows マルチメディア機能[**mixerGetLineControls**](https://docs.microsoft.com/previous-versions/dd757302(v=vs.85))を使用して、ミキサーコントロールにアクセスできます。 この関数は、1つまたは複数の MIXERCONTROL 構造体の配列を取得します。各構造体は、オーディオ回線上の単一のコントロールノードの状態とメトリックを記述します。 MIXERCONTROL 構造体の**Dwcontroltype**メンバーは、コントロールの種類を指定する列挙値に設定されます。 オーディオ Vxd にはいくつかのミキサーコントロール型が指定されていますが、WDM オーディオドライバーで使用できるのはこれらのコントロールのサブセットのみです。

WDMAud は、一部のトポロジノードを対応するミキサーラインコントロールに変換します。 次の表に示すトポロジノードの種類には、ミキサーラインコントロールである対応するものがあります。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ノードの種類</th>
<th align="left">トポロジ-ノードタイプ名</th>
<th align="left">ミキサー-コントロールの型名</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>AGC</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-agc" data-raw-source="[&lt;strong&gt;KSNODETYPE_AGC&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-agc)"><strong>KSNODETYPE_AGC</strong></a></p></td>
<td align="left"><p>MIXERCONTROL_CONTROLTYPE_ONOFF</p></td>
</tr>
<tr class="even">
<td align="left"><p>等</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-loudness" data-raw-source="[&lt;strong&gt;KSNODETYPE_LOUDNESS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-loudness)"><strong>KSNODETYPE_LOUDNESS</strong></a></p></td>
<td align="left"><p>MIXERCONTROL_CONTROLTYPE_LOUDNESS</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Mute</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-mute" data-raw-source="[&lt;strong&gt;KSNODETYPE_MUTE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-mute)"><strong>KSNODETYPE_MUTE</strong></a></p></td>
<td align="left"><p>MIXERCONTROL_CONTROLTYPE_MUTE</p></td>
</tr>
<tr class="even">
<td align="left"><p>声調 (複数)</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-tone" data-raw-source="[&lt;strong&gt;KSNODETYPE_TONE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-tone)"><strong>KSNODETYPE_TONE</strong></a></p></td>
<td align="left"><p>MIXERCONTROL_CONTROLTYPE_ONOFF (KSPROPERTY_AUDIO_BASS_BOOST がサポートされている場合)</p>
<p>MIXERCONTROL_CONTROLTYPE_BASS (KSPROPERTY_AUDIO_BASS がサポートされている場合)</p>
<p>MIXERCONTROL_CONTROLTYPE_TREBLE (KSPROPERTY_AUDIO_TREBLE がサポートされている場合)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>[ボリューム]</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-volume" data-raw-source="[&lt;strong&gt;KSNODETYPE_VOLUME&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-volume)"><strong>KSNODETYPE_VOLUME</strong></a></p></td>
<td align="left"><p>MIXERCONTROL_CONTROLTYPE_VOLUME</p></td>
</tr>
<tr class="even">
<td align="left"><p>Peakmeter</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-peakmeter" data-raw-source="[&lt;strong&gt;KSNODETYPE_PEAKMETER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-peakmeter)"><strong>KSNODETYPE_PEAKMETER</strong></a></p></td>
<td align="left"><p>MIXERCONTROL_CONTROLTYPE_PEAKMETER</p></td>
</tr>
<tr class="odd">
<td align="left"><p>マルチプレクサー</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-mux" data-raw-source="[&lt;strong&gt;KSNODETYPE_MUX&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-mux)"><strong>KSNODETYPE_MUX</strong></a></p></td>
<td align="left"><p>MIXERCONTROL_CONTROLTYPE_MUX</p></td>
</tr>
<tr class="even">
<td align="left"><p>ステレオワイド</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-stereo-wide" data-raw-source="[&lt;strong&gt;KSNODETYPE_STEREO_WIDE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-stereo-wide)"><strong>KSNODETYPE_STEREO_WIDE</strong></a></p></td>
<td align="left"><p>MIXERCONTROL_CONTROLTYPE_FADER</p></td>
</tr>
<tr class="odd">
<td align="left"><p>コーラス</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-chorus" data-raw-source="[&lt;strong&gt;KSNODETYPE_CHORUS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-chorus)"><strong>KSNODETYPE_CHORUS</strong></a></p></td>
<td align="left"><p>MIXERCONTROL_CONTROLTYPE_FADER</p></td>
</tr>
<tr class="even">
<td align="left"><p>ほど</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-reverb" data-raw-source="[&lt;strong&gt;KSNODETYPE_REVERB&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-reverb)"><strong>KSNODETYPE_REVERB</strong></a></p></td>
<td align="left"><p>MIXERCONTROL_CONTROLTYPE_FADER</p></td>
</tr>
<tr class="odd">
<td align="left"><p>スーパーミックス (複数)</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-supermix" data-raw-source="[&lt;strong&gt;KSNODETYPE_SUPERMIX&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-supermix)"><strong>KSNODETYPE_SUPERMIX</strong></a></p></td>
<td align="left"><p>MIXERCONTROL_CONTROLTYPE_MUTE (KSPROPERTY_AUDIO_MUTE がスーパーミックスノードでサポートされている場合)</p>
<p>MIXERCONTROL_CONTROLTYPE_VOLUME (テキスト内のコメントを参照)</p></td>
</tr>
</tbody>
</table>

 

上の表にないトポロジノードの種類は、ミキサーラインコントロールには変換されません。また、テーブルにないミキサーラインコントロールは、WDM オーディオドライバーではサポートされていません。

MIXERCONTROL\_CONTROLTYPE\_カスタムがテーブルに存在しないことに注意してください。 これは、WDM オーディオドライバーがカスタムミキサーコントロールをサポートしていないことを意味します。

[**トーンノード**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-tone)では、[**低音**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-bass)、[**高音**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-treble)、[**ミッド周波数**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-mid)、[**低音ブースト**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-bass-boost)の4つのプロパティがサポートされています。 Mid frequency プロパティには、対応するミキサー線はありませんが、他の3つのプロパティは実行します。 トポロジで検出された各トーンノードについて、サポートされる各プロパティに対してクエリが実行されます。

[**KSK プロパティ\_AUDIO\_低音**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-bass)

[**KSK プロパティ\_オーディオ\_高音**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-treble)

[**KSK プロパティ\_オーディオ\_低音\_ブースト**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-bass-boost)

成功した各プロパティクエリでは、ミキサーラインコントロールが生成されます。 名前付けの問題により、1つの声調ノードは1つのプロパティのみをサポートする必要があります。 たとえば、デバイスが低音と高音の両方をサポートしている場合は、ノードが異なる名前を持つことができるように、2つの声調ノードが必要です。

[**スーパーミックスノード**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-supermix)では、ミュートとボリュームの2つまでのコントロールがサポートされています。 スーパーミックスノードの[**機能テーブル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_mixcap_table)内の各エントリに対して、次の2つの条件のうち少なくとも1つを満たす場合は、ミュートコントロールとして使用できます。

-   エントリは、**機能**によって指定されたミュートプロパティをサポートしています。**ミュート**フラグ。

-   エントリは完全に減衰されています (-無限大デシベル減衰)。このエントリは、両方の**機能**で指定されているため、起動できません。**最小**および**機能**。**最大**値が LONG\_MIN (0x80000000)。

スーパーミックス機能テーブルのすべてのエントリに0以外の範囲がある場合は、スーパーミックスノードをボリュームコントロールとして使用できます。 他のすべてのコントロールは1対1で変換されます。 認識されたノードが検出されると、ミキサーラインドライバーはそのノードの各プロパティに対してクエリを行います。

ステレオまたは mono のサポートを確認するには、左側のチャネルに対してクエリを実行し、次に右のチャネルを使用します。最後に、両方のチャネルで障害が発生した場合、マスターチャネル (-1) が試行されます。 これらのクエリのいずれも成功しない場合、そのノードのコントロールは生成されません。 MUX ノードはチャネルごとに照会されないことに注意してください。 代わりに、現在の MUX 選択を取得するための1つのクエリが実行されます。

コントロールの名前は、その[**ksproperty\_TOPOLOGY\_name**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-topology-name)プロパティに対してノードが照会されると、文字列として返されます。 ノードが複数のコントロールを生成する場合、すべてのコントロールが同じ名前を共有します。

 

 




