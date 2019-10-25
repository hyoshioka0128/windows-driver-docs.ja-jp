---
title: KSK プロパティ\_接続\_DATAFORMAT
description: クライアントは、KSK プロパティ\_接続\_DATAFORMAT プロパティを使用して、現在のデータ形式を設定します。
ms.assetid: c5f37f1b-7dc6-46d2-aba2-b6c03f07228d
keywords:
- KSPROPERTY_CONNECTION_DATAFORMAT ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CONNECTION_DATAFORMAT
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5aa1e35d2ecf6fe5d855f7a3e24c84af6543d404
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826797"
---
# <a name="ksproperty_connection_dataformat"></a>KSK プロパティ\_接続\_DATAFORMAT


クライアントは、KSK プロパティ\_接続\_DATAFORMAT プロパティを使用して、現在のデータ形式を設定します。

## <span id="ddk_ksproperty_connection_dataformat_ks"></span><span id="DDK_KSPROPERTY_CONNECTION_DATAFORMAT_KS"></span>


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
<td><p>必須ではない</p></td>
<td><p>[はい]</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat" data-raw-source="[&lt;strong&gt;KSDATAFORMAT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)"><strong>KSDATAFORMAT</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

このプロパティは、要求されたデータ形式を指定する[**KSDATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)構造体を受け取ります。

KS フィルターでは、クライアントが現在のプロパティをリセットすることを許可している場合、またはデータ形式が不完全な場合に接続を確立できる場合にのみ、このプロパティをサポートする必要があります。

DATAFORMAT プロパティの KSK プロパティ\_接続\_の詳細については、「 [KS データ形式とデータ](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-data-formats-and-data-ranges)範囲」と「データ[範囲の積集合 (avstream](https://docs.microsoft.com/windows-hardware/drivers/stream/data-range-intersections-in-avstream))」を参照してください。

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


[**KSK ストリーム\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header)

[**KSK プロパティ\_接続\_PROPOSEDATAFORMAT**](ksproperty-connection-proposedataformat.md)

[**KSK プロパティ\_PIN\_PROPOSEDATAFORMAT**](ksproperty-pin-proposedataformat.md)

 

 






