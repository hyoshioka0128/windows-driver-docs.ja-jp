---
title: KSPROPERTY\_AUDIOENGINE\_ループバック\_保護
description: KSPROPERTY\_AUDIOENGINE\_ループバック\_保護プロパティ要求により、オーディオ ドライバー、オーディオ エンジン ノードのループバック保護の状態を設定します。
ms.assetid: E798582C-7662-413C-B25C-6A129FDEEE38
keywords:
- KSPROPERTY_AUDIOENGINE_LOOPBACK_PROTECTION オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIOENGINE_LOOPBACK_PROTECTION
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6de57599601cfbb434ab859330d2ab0c587b88a1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332799"
---
# <a name="kspropertyaudioengineloopbackprotection"></a>KSPROPERTY\_AUDIOENGINE\_ループバック\_保護


**KSPROPERTY\_AUDIOENGINE\_ループバック\_保護**プロパティ要求により、オーディオ ドライバー、オーディオ エンジン ノードのループバック保護の状態を設定します。

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
<td align="left"><p>X</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>暗証番号 (pin) のインスタンスを使用してノード</p></td>
<td align="left"><p>KSP_NODE</p></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_AUDIOENGINE\_ループバック\_保護プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

このプロパティの呼び出しに関連付けられている入力バッファーには、型 CONSTRICTOR の列挙値が設定されます\_オプション。 入力バッファーが CONSTRICTOR を設定するか、\_オプション\_無効化または CONSTRICTOR\_オプション\_ミュートします。

CONSTRICTOR で作業中のストリームがある場合\_オプション\_このオーディオ出力の KS ループバック タップはサイレント状態を出力し、実際には、ミュートします。 アクティブなすべてのストリームが CONSTRICTOR\_オプション\_だけを (つまり、既定の状態) 有効では、無効にし、ループバック タップは、意味のあるデータを含みます。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows 8</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**KSPROPERTY\_AUDIOENGINE**](ksproperty-audioengine.md)

 

 






