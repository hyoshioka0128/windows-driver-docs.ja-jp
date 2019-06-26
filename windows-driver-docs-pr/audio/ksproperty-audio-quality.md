---
title: KSPROPERTY\_オーディオ\_品質
description: KSPROPERTY\_オーディオ\_品質プロパティ ノードの出力ストリームの品質レベルを指定します。 これは、SRC ノードのプロパティ (KSNODETYPE\_SRC)。
ms.assetid: ef57de3b-f7ac-4ecd-915e-27f34fcc2028
keywords:
- KSPROPERTY_AUDIO_QUALITY オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_QUALITY
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ef1a3d41cb63c942c4cfee0c778e7383aa6f66c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358889"
---
# <a name="kspropertyaudioquality"></a>KSPROPERTY\_オーディオ\_品質


KSPROPERTY\_オーディオ\_品質プロパティ ノードの出力ストリームの品質レベルを指定します。 これは、SRC ノードのプロパティ ([**KSNODETYPE\_SRC**](ksnodetype-src.md))。

## <span id="ddk_ksproperty_audio_quality_ks"></span><span id="DDK_KSPROPERTY_AUDIO_QUALITY_KS"></span>


### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">取得</th>
<th align="left">設定</th>
<th align="left">対象</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>〇</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は ULONG 型で、出力ストリームの品質レベルを指定します。 この値は、ヘッダー ファイル Ksmedia.h から、次の定数のいずれかに設定する必要があります。

<span id="KSAUDIO_QUALITY_WORST"></span><span id="ksaudio_quality_worst"></span>KSAUDIO\_品質\_最悪  
最悪の品質

<span id="KSAUDIO_QUALITY_PC"></span><span id="ksaudio_quality_pc"></span>KSAUDIO\_品質\_PC  
(による制約のない) 標準的なコンピューターの品質

<span id="KSAUDIO_QUALITY_BASIC"></span><span id="ksaudio_quality_basic"></span>KSAUDIO\_品質\_BASIC  
基本的な (下位) コンシューマー オーディオの品質 (既定値)

<span id="KSAUDIO_QUALITY_ADVANCED"></span><span id="ksaudio_quality_advanced"></span>KSAUDIO\_品質\_[詳細設定]  
高度な (ハイエンド) コンシューマー オーディオ品質

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_オーディオ\_品質プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

サンプル レートの変換の種類についてを[KMixer システム ドライバー](https://docs.microsoft.com/windows-hardware/drivers/audio/kernel-mode-wdm-audio-components#kmixer-system-driver)実行するを参照してください[KMixer ドライバーのサンプル レートの変換との混合ポリシー](https://docs.microsoft.com/windows-hardware/drivers/audio/kmixer-driver-sample-rate-conversion-and-mixing-policy)します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**KSNODETYPE\_SRC**](ksnodetype-src.md)

[**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty)

 

 






