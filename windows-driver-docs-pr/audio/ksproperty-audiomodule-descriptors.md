---
title: KSK プロパティ\_AUDIOMODULE\_記述子
description: KSK プロパティ\_AUDIOMODULE\_記述子は、エンドポイント wave フィルターの各オーディオモジュールの静的データ記述子を取得するために使用されます。
ms.assetid: EAD613AA-005B-4751-B60E-212853CA40B4
keywords:
- KSPROPERTY_AUDIOMODULE_DESCRIPTORS オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIOMODULE_DESCRIPTORS
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10da8d7b34c6f92dc2d8743797075feeca9dbba1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830843"
---
# <a name="ksproperty_audiomodule_descriptors"></a>KSK プロパティ\_AUDIOMODULE\_記述子


**Ksk プロパティ\_audiomodule\_記述子**は、エンドポイント wave フィルターの各オーディオモジュールの静的データ記述子を取得するために使用されます。

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

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
<th align="left">[購入]</th>
<th align="left">設定</th>
<th align="left">対象</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>[はい]</p></td>
<td align="left"><p>必須ではない</p></td>
<td align="left"><p>フィルターまたはピン留め</p></td>
<td align="left"><p><strong>KSPROPERTY</strong></p></td>
<td align="left"><p>フィルターターゲットの場合は、KSMULTIPLE_ITEM の後に、テンプレートモジュールを記述する KSAUDIOMODULE_DESCRIPTOR の配列。</p>
<p>ピンターゲットの場合、KSMULTIPLE_ITEM の後に、そのストリームパス内のインスタンス化されたモジュールの KSAUDIOMODULE_DESCRIPTOR の配列が続きます。</p></td>
</tr>
</tbody>
</table>

 

プロパティ値は構造体であり、その後にゼロ (0) 以上の[**KSAUDIOMODULE\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksaudiomodule_descriptor)構造体が続きます。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

**Ksk プロパティ\_AUDIOMODULE\_記述子**は、この要求への応答としてこれらの記述子の配列を返します。

ドライバーがこのプロパティをサポートしていても、オーディオモジュールがない場合は、要素数が0である ksmultiple\_項目を返します。

オーディオモジュールの詳細については、「[オーディオモジュール検出の実装](https://docs.microsoft.com/windows-hardware/drivers/audio/implementing-audio-module-communication)」を参照してください。

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
<td align="left"><p>Windows 10 バージョン1703</p></td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**KSAUDIOMODULE\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksaudiomodule_descriptor)

[KSPROPSETID\_AudioModule](kspropsetid-audiomodule.md)

 

 






