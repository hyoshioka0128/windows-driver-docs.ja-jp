---
title: KSK プロパティ\_SOUNDDETECTOR\_SUPPORTEDPATTERNS
description: サポートされ\_ている\_パターンの種類を識別する guid の一覧を取得するには、ksk プロパティの sounddetector supportedpatterns プロパティを使用します。
ms.assetid: 8D840204-ADE8-4146-B88C-C0750B8FC33A
keywords:
- KSPROPERTY_SOUNDDETECTOR_SUPPORTEDPATTERNS オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_SOUNDDETECTOR_SUPPORTEDPATTERNS
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 09/25/2019
ms.localizationpriority: medium
ms.openlocfilehash: a66699736e788844a1becfa2b6e5d5a938ad0360
ms.sourcegitcommit: 8295a2b59212972b0f7457a748cc904b5417ad67
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71319917"
---
# <a name="ksproperty_sounddetector_supportedpatterns"></a>KSK プロパティ\_SOUNDDETECTOR\_SUPPORTEDPATTERNS

サポートされているパターンの種類を識別する guid の一覧を取得するには、 **ksk プロパティ\_の\_sounddetector supportedpatterns**プロパティを使用します。

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table---kspropsetid_sounddetector"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル-KSPROPSETID_SoundDetector

この使用状況テーブルは、 [KSPROPSETID_SoundDetector](kspropsetid-sounddetector.md)を使用\_して、ksproperty\_の sounddetector 機が呼び出されるタイミングをまとめたものです。

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
<th align="left">Set</th>
<th align="left">移行先</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>はい</p></td>
<td align="left"><p>いいえ</p></td>
<td align="left"><p>Assert</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksmultiple_item" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksmultiple_item)"><strong>KSMULTIPLE_ITEM</strong></a></p></td>
</tr>
</tbody>
</table>

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table---kspropsetid_sounddetector2"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル-KSPROPSETID_SoundDetector2

この使用状況テーブルは、 [KSPROPSETID_SoundDetector2](kspropsetid-sounddetector2.md)を使用\_して、ksproperty\_の sounddetector 機が呼び出されるタイミングをまとめたものです。

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
<th align="left">Set</th>
<th align="left">移行先</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>はい</p></td>
<td align="left"><p>いいえ</p></td>
<td align="left"><p>Assert</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-kssounddetectorproperty" data-raw-source="[&lt;strong&gt;KSSOUNDDETECTORPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-kssounddetectorproperty"><strong>KSSOUNDDETECTORPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksmultiple_item" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksmultiple_item)"><strong>KSMULTIPLE_ITEM</strong></a></p></td>
</tr>
</tbody>
</table>

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

プロパティ値は、 [ **\_ksmultiple ITEM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksmultiple_item)構造体の後に一連の guid が続きます。

<a name="remarks"></a>コメント
-------

パターン GUID には、次の特性があります。

- これは OEM によって生成されます。

- オペレーティングシステムは、これをクラス識別子 (CLSID) として使用し、ドライバーとの対話に使用される、対応する OEM DLL COM クラスをインスタンス化します。

- これは、OEM によって定義されるパターンデータの形式を意味します。

- これは、OEM によって定義された結果データの形式を意味します。

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
<td align="left"><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**KSPROPERTY**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))

[**KSMULTIPLE\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksmultiple_item)
