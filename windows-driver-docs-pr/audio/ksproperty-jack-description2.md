---
title: KSPROPERTY\_ジャック\_DESCRIPTION2
description: KSPROPERTY\_ジャック\_DESCRIPTION2 プロパティは、フィルターのハンドルを使用してアクセスされる pin-wise プロパティとして実装されます。
ms.assetid: 6856060b-f735-4ed8-99bd-5896c87d581f
keywords:
- KSPROPERTY_JACK_DESCRIPTION2 オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_JACK_DESCRIPTION2
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 774bff3c399110ed435f7e75fa8d71b0625cb9f5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358767"
---
# <a name="kspropertyjackdescription2"></a>KSPROPERTY\_ジャック\_DESCRIPTION2


KSPROPERTY\_ジャック\_DESCRIPTION2 プロパティは、フィルターのハンドルを使用してアクセスされる pin-wise プロパティとして実装されます。

Windows 7 およびそれ以降の Windows オペレーティング システムでこのプロパティは、1 つまたは複数の物理ジャックに関連付けられているブリッジ暗証番号 (pin) をサポートできます。 KSPROPERTY\_ジャック\_DESCRIPTION2 を使用して、状態とデバイスのジャックに関連する機能を取得します。

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
<td align="left"><p>(フィルターのハンドル) を使用してファクトリをピン留めします。</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_pin" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_pin)"><strong>KSP_PIN</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksmultiple_item" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksmultiple_item)"><strong>KSMULTIPLE_ITEM</strong> </a>の配列を続けて<a href="ksjack-description2.md" data-raw-source="[&lt;strong&gt;KSJACK_DESCRIPTION2&lt;/strong&gt;](ksjack-description2.md)"> <strong>KSJACK_DESCRIPTION2</strong> </a>構造体</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (インスタンス データ) は、KSMULTIPLE\_KSJACK の配列で\_DESCRIPTION2 構造体。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_ジャック\_DESCRIPTION2 プロパティ要求が、KSMULTIPLE を返します\_項目配列の後に*N* KSJACK\_DESCRIPTION2 構造体、 *N* = 指定したブリッジの暗証番号 (pin) に関連付けられているジャックの数。 プロパティ要求によって返される項目を次に示します。

KSMULTIPLE\_項目。サイズ = sizeof (KSMULTIPLE\_項目) + N \* sizeof (KSJACK\_DESCRIPTION2)

KSMULTIPLE\_ITEM.Count = N

KSJACK\_DESCRIPTION2\[0\]

...

KSJACK\_DESCRIPTION2\[N-1\]

<a name="remarks"></a>注釈
-------

各 KSJACK\_DESCRIPTION2 構造は、1 つのジャックに関する情報を含める必要がありますのみです。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>サポートされている最小のクライアント</p></td>
<td align="left"><p>Windows 7</p></td>
</tr>
<tr class="even">
<td align="left"><p>サポートされている最小のサーバー</p></td>
<td align="left"><p>Windows Server 2008</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**KSJACK\_DESCRIPTION2**](ksjack-description2.md)

[KSMULTIPLE\_項目](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksmultiple_item)

 

 






