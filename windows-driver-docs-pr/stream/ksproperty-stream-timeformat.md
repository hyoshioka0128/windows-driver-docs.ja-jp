---
title: KSK プロパティ\_STREAM\_TIMEFORMAT
description: KSK プロパティ\_STREAM\_TIMEFORMAT プロパティは、特定のピン接続で使用される時刻形式を取得するために使用されます。
ms.assetid: bf8c32b2-401f-4f89-bcca-97a07c50cc45
keywords:
- KSPROPERTY_STREAM_TIMEFORMAT ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_STREAM_TIMEFORMAT
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 58a3e7b4a410a004e1e0f46ad1259a1209ec4ae6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837937"
---
# <a name="ksproperty_stream_timeformat"></a>KSK プロパティ\_STREAM\_TIMEFORMAT


KSK プロパティ\_STREAM\_TIMEFORMAT プロパティは、特定のピン接続で使用される時刻形式を取得するために使用されます。

## <span id="ddk_ksproperty_stream_timeformat_ks"></span><span id="DDK_KSPROPERTY_STREAM_TIMEFORMAT_KS"></span>


### <a name="usage-summary-table"></a>使用状況の概要テーブル

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
<th>[購入]</th>
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>[はい]</p></td>
<td><p>必須ではない</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p>GUID</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

プロパティは、接続で使用される時刻形式を指定し、プレゼンテーション時間と範囲の形式を示す GUID を返します。 定義された時間形式は、DirectShow によって定義された時刻に対応します。

KSK プロパティ\_STREAM\_TIMEFORMAT は省略可能なプロパティであり、pin がレート、プレゼンテーションの時間/範囲、または低下のプロパティをスキップする場合に実装する必要があります (これらのプロパティの詳細については、「Quality」を参照してください)。 [管理](https://docs.microsoft.com/windows-hardware/drivers/stream/quality-management))。 これにより、クライアントは、接続に使用される時刻形式と、速度、プレゼンテーション時間/範囲、および [低下のスキップ] 操作に使用されるタイムスタンプ情報の形式を決定できます。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ks (Ks を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

 

 






