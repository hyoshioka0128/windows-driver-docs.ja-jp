---
title: KSK プロパティ\_テレフォニー\_ENDPOINTIDPAIR
description: KSK プロパティ\_TELEPHONY\_ENDPOINTIDPAIR プロパティには、携帯電話のオーディオルーティング用のレンダーおよびキャプチャのエンドポイントが含まれています。
ms.assetid: 4F163A65-5572-41D0-80B2-493285E2B87B
keywords:
- KSPROPERTY_TELEPHONY_ENDPOINTIDPAIR オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_TELEPHONY_ENDPOINTIDPAIR
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0140347ede505437ad1503ac40ffef186f76058a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832685"
---
# <a name="ksproperty_telephony_endpointidpair"></a>KSK プロパティ\_テレフォニー\_ENDPOINTIDPAIR


**Ksk プロパティ\_TELEPHONY\_ENDPOINTIDPAIR**プロパティには、携帯電話のオーディオルーティング用のレンダーおよびキャプチャのエンドポイントが含まれています。

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
<td align="left"><p>[はい]</p></td>
<td align="left"><p>フィルター</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagkstopology_endpointidpair" data-raw-source="[&lt;strong&gt;KSTOPOLOGY_ENDPOINTIDPAIR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagkstopology_endpointidpair)"><strong>KSTOPOLOGY_ENDPOINTIDPAIR</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ値の型は[**Ksto\_POENDPOINTIDPAIR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagkstopology_endpointidpair)で、レンダリングエンドポイントとキャプチャエンドポイントを指定します。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

**Ksk プロパティ\_TELEPHONY\_ENDPOINTIDPAIR** property 要求は、携帯電話のオーディオルーティングのレンダーおよびキャプチャのエンドポイントを返します。

<a name="remarks"></a>注釈
-------

移動体通信ルーティングは、トポロジフィルターの**ENDPOINTIDPAIR プロパティ\_\_の Ksk プロパティ**によって制御されます。 このプロパティは、要求されたエンドポイントの組み合わせに対して、 [**Kstopology\_ENDPOINTID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagkstopology_endpointid)構造体のペアを受け取ります。 **Kstopology\_ENDPOINTID**は、エンドポイントのトポロジフィルターの参照文字列と、エンドポイントが接続されているトポロジフィルターの pin ID を含みます。 このドライバーは、このプロパティの基本的なサポートを提供し、携帯電話のオーディオルーティングに使用できるレンダーおよびキャプチャエンドポイントのすべての有効なペアを返します。 この新しいエンドポイントの組み合わせに対しては、レンダリングとキャプチャの両方のオーディオの移動を処理する必要があり、ハードウェアに必要な制約をすべて満たしています。 このプロパティは、システムにアクティブな通話がない場合でも設定可能でなければなりません。

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
<td align="left"><p>クライアント</p></td>
<td align="left"><p>Windows 10 Mobile</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

 

 





