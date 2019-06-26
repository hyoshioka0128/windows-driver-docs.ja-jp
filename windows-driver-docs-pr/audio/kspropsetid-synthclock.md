---
title: KSPROPSETID\_SynthClock
description: KSPROPSETID\_SynthClock
ms.assetid: 8baad0d2-ea86-4d27-8fb0-03cdd9e978f0
keywords:
- KSPROPSETID_SynthClock
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c9aa608d324bb72650cedc24eee2f443c581611
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391554"
---
# <a name="kspropsetidsynthclock"></a>KSPROPSETID\_SynthClock


## <span id="ddk_kspropsetid_synthclock_ks"></span><span id="DDK_KSPROPSETID_SYNTHCLOCK_KS"></span>


`KSPROPSETID_SynthClock`プロパティ セットを使用して、DirectMusic シンセサイザーをマスターのクロック時間を取得します。 このセットには、DirectMusic フィルター オブジェクトの 1 つのプロパティが含まれています。 Dmu ポート ドライバーでは、このプロパティのハンドラーを実装します。

詳細については、次を参照してください。[マスター クロック](https://docs.microsoft.com/windows-hardware/drivers/stream/master-clocks)と[シンセサイザー タイミング](https://docs.microsoft.com/windows-hardware/drivers/audio/synthesizer-timing)します。

このセット内のプロパティ項目が KSPROPERTY によって指定された\_SYNTHCLOCK 列挙値では、ヘッダーで定義されているファイル Dmusprop.h します。

## <span id="ddk_ksproperty_synth_masterclock_ks"></span><span id="DDK_KSPROPERTY_SYNTH_MASTERCLOCK_KS"></span>


### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

KSPROPERTY\_シンセサイザー\_MASTERCLOCK プロパティを使用して、マスターのクロック時間を取得します。

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
<td align="left"><p>フィルター</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p>ULONGLONG</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は ULONGLONG 型で、マスターのクロック時間を表します。 この時間は 100 ナノ秒単位で指定されます。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_シンセサイザー\_MASTERCLOCK プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

詳細については、次を参照してください。[マスター クロック](https://docs.microsoft.com/windows-hardware/drivers/stream/master-clocks)します。

 

 





