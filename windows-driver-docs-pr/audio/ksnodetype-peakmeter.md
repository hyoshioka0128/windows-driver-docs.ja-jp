---
title: KSNODETYPE\_PEAKMETER
description: KSNODETYPE\_PEAKMETER
ms.assetid: 11c886eb-dd63-44dd-9bca-dd19a8dd6948
keywords:
- KSNODETYPE_PEAKMETER オーディオデバイス
topic_type:
- apiref
api_name:
- KSNODETYPE_PEAKMETER
api_type:
- NA
ms.date: 04/21/2020
ms.localizationpriority: medium
ms.openlocfilehash: 8ab731f662f2efaa2785bc9bcbd8d609b7993aa9
ms.sourcegitcommit: 8f27122409dea11ef0635afbbe5788a648066a1a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2020
ms.locfileid: "81772737"
---
# <a name="ksnodetype_peakmeter"></a>KSNODETYPE\_PEAKMETER

## <span id="ddk_ksnodetype_peakmeter_ks"></span><span id="DDK_KSNODETYPE_PEAKMETER_KS"></span>

**KSNODETYPE\_peakmeter**ノードは、ハードウェア peakmeter を表します。 KS peakmeter ノードには1つの入力ピンと1つの出力ピンがあり、2つのピンは同じデータ形式を共有します。

KS peakmeter は、最後に peakmeter がゼロにリセットされた後のオーディオ信号の最大値を内部的にログに記録します。 Peakmeter は、 [**ksk プロパティ\_AUDIO\_PEAKMETER2**](ksproperty-audio-peakmeter2.md)プロパティを取得\_する\_ために、IOCTL KS プロパティの要求の後に自動的に0にリセットされます。

Peakmeter では、ハードウェアのサポートが必要です。 ソフトウェアの peakmeter は実現可能ではありません。これは、アダプタードライバーが、再生チャネルと混合されている、ライン入力、マイク、またはその他の入力に存在する信号にアクセスできないためです。

Microsoft では、フィルター内でストリームが渡される最後のノードに peakmeter ノードを作成することをお勧めします。 レンダリングストリームでは、通常、オーディオアダプターはマスター出力[**KSNODETYPE\_ミュート**](ksnodetype-mute.md)ノードまたは[**KSNODETYPE\_ボリューム**](ksnodetype-volume.md)ノードの後に peakmeter ノードを接続します。 この方法は、キャプチャストリームまたはフィルターに peakmeter ノードが組み込まれているその他のストリームにも当てはまります。

オーディオアダプターは、peakmeter ノード KSK の名前\_を peakmeter にする必要があります。

Peakmeter ノードでは、次の表に示すプロパティフラグ ( [**Ksk プロパティ**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))を参照) のプロパティハンドラーが提供されている必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">フラグ名</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>KSPROPERTY_TYPE_GET</p></td>
<td align="left"><p>ハードウェアの peakmeter の現在の値を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSPROPERTY_TYPE_BASICSUPPORT</p></td>
<td align="left"><p>
KSPROPERTY_AUDIO_PEAKMETER-では、0x8000 から、16ビットのデジタルオーディオのデータ範囲である0x8000 までのデータ範囲が返されます。 オペレーティングシステムが正の値を受け取ることができるように、上位16ビットを0に設定する必要があります。 KSPROPERTY_AUDIO_PEAKMETER は非推奨とされ、代わりに KSPROPERTY_AUDIO_PEAKMETER2 を使用する必要があることに注意してください。</p>
<p>KSPROPERTY_AUDIO_PEAKMETER2-LONG_MAX する LONG_MIN のデータ範囲を返します。</p>
</td>
</tr>
</tbody>
</table>

プロパティハンドラーは、入力パラメーターと左および右のチャネル情報を検証する必要があります。

Peakmeter ノードでは、次の表のプロパティもサポートする必要があります。

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
<td align="left"><p><a href="ksproperty-audio-peakmeter2.md" data-raw-source="[&lt;strong&gt;KSPROPERTY_AUDIO_PEAKMETER2&lt;/strong&gt;](ksproperty-audio-peakmeter2.md)"><strong>KSPROPERTY_AUDIO_PEAKMETER2</strong></a></p></td>
<td align="left"><p>Peakmeter コントロールを表します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ksproperty-audio-cpu-resources.md" data-raw-source="[&lt;strong&gt;KSPROPERTY_AUDIO_CPU_RESOURCES&lt;/strong&gt;](ksproperty-audio-cpu-resources.md)"><strong>KSPROPERTY_AUDIO_CPU_RESOURCES</strong></a></p></td>
<td align="left"><p>指定したノードの機能がホストの CPU を使用しているかどうかを示します。</p></td>
</tr>
</tbody>
</table>
