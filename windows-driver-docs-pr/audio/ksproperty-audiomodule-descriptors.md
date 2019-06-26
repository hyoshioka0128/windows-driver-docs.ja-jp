---
title: KSPROPERTY\_AUDIOMODULE\_記述子
description: KSPROPERTY\_AUDIOMODULE\_記述子を使用するエンドポイント波形のフィルターの各オーディオ モジュールに静的なデータ記述子を取得します。
ms.assetid: EAD613AA-005B-4751-B60E-212853CA40B4
keywords:
- KSPROPERTY_AUDIOMODULE_DESCRIPTORS オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIOMODULE_DESCRIPTORS
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: dfa2a9be1707fddbeaccd8631c15a64dd5bcf72f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358844"
---
# <a name="kspropertyaudiomoduledescriptors"></a>KSPROPERTY\_AUDIOMODULE\_記述子


**KSPROPERTY\_AUDIOMODULE\_記述子**が使用するエンドポイント波形のフィルターの各オーディオ モジュールに静的なデータ記述子を取得します。

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
<td align="left"><p>X</p></td>
<td align="left"><p>フィルターまたはピン留めします。</p></td>
<td align="left"><p><strong>KSPROPERTY</strong></p></td>
<td align="left"><p>フィルター対象のテンプレートのモジュールを記述する KSAUDIOMODULE_DESCRIPTOR の配列を続けて KSMULTIPLE_ITEM します。</p>
<p>暗証番号 (pin) 対象のインスタンス化されたモジュールは、そのストリーム パス KSAUDIOMODULE_DESCRIPTOR の配列を続けて KSMULTIPLE_ITEM。</p></td>
</tr>
</tbody>
</table>

 

プロパティの値は、構造体は、ゼロ (0) 以上続く[ **KSAUDIOMODULE\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ksaudiomodule_descriptor)構造体。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

**KSPROPERTY\_AUDIOMODULE\_記述子**これらの記述子の配列は、この要求に応答で返されるを返します。

返します、ksmultiple、ドライバーは、このプロパティをサポート、オーディオのすべてのモジュールがない場合は、\_0 個の要素数を持つ項目。

オーディオのモジュールの詳細については、次を参照してください。[オーディオ モジュールの検出を実装する](https://docs.microsoft.com/windows-hardware/drivers/audio/implementing-audio-module-communication)します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>サポートされている最小のクライアント</p></td>
<td align="left"><p>Windows 10</p></td>
</tr>
<tr class="even">
<td align="left"><p>サポートされている最小のサーバー</p></td>
<td align="left"><p>サポートなし</p></td>
</tr>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows 10 バージョン 1703</p></td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**KSAUDIOMODULE\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ksaudiomodule_descriptor)

[KSPROPSETID\_AudioModule](kspropsetid-audiomodule.md)

 

 






