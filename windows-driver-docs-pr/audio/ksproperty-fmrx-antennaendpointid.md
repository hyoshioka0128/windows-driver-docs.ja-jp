---
title: KSPROPERTY\_FMRX\_ANTENNAENDPOINTID
description: KSTOPOLOGY\_ENDPOINTID プロパティには、FM アンテナとして使用されるエンドポイントに関する情報が含まれています。
ms.assetid: 96B831E8-2372-413E-A9DE-63248F4F5863
keywords:
- KSPROPERTY_FMRX_ANTENNAENDPOINTID オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_FMRX_ANTENNAENDPOINTID
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 116a8ff4dff3d85d9fecf975f69c8ac4a7571491
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832766"
---
# <a name="ksproperty_fmrx_antennaendpointid"></a>KSPROPERTY\_FMRX\_ANTENNAENDPOINTID


[**Kstopology\_ENDPOINTID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagkstopology_endpointid)プロパティには、FM アンテナとして使用されるエンドポイントに関する情報が含まれています。

## <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル


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
<td align="left"><p>フィルター</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagkstopology_endpointid" data-raw-source="[&lt;strong&gt;KSTOPOLOGY_ENDPOINTID&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagkstopology_endpointid)"><strong>KSTOPOLOGY_ENDPOINTID</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ値の型は[**Kstopology\_ENDPOINTID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagkstopology_endpointid)で、FM ラジオ受信アンテナに関連付けられているトポロジエンドポイントの名前と pin ID を指定します。

## <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値


KSK プロパティ\_FMRX\_ANTENNAENDPOINTID property 要求は、FM ラジオアンテナとして使用されるエンドポイントの名前と pin id を返します。

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
<td align="left"><p>クライアント</p></td>
<td align="left"><p>Windows 10 Mobile</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

 

 





