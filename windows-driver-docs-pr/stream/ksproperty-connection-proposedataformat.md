---
title: KSK プロパティ\_接続\_PROPOSEDATAFORMAT
description: クライアントは、KSK プロパティ\_接続\_PROPOSEDATAFORMAT プロパティを使用して、接続用の新しいデータ形式を提案できます。
ms.assetid: f5bc7cd2-0033-4761-962b-33c82925134b
keywords:
- KSPROPERTY_CONNECTION_PROPOSEDATAFORMAT ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CONNECTION_PROPOSEDATAFORMAT
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 46f00feeaf41cf15ce145b3deeafcffef7a4998d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826786"
---
# <a name="ksproperty_connection_proposedataformat"></a>KSK プロパティ\_接続\_PROPOSEDATAFORMAT


クライアントは、KSK プロパティ\_接続\_PROPOSEDATAFORMAT プロパティを使用して、接続用の新しいデータ形式を提案できます。

## <span id="ddk_ksproperty_connection_proposedataformat_ks"></span><span id="DDK_KSPROPERTY_CONNECTION_PROPOSEDATAFORMAT_KS"></span>


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

このプロパティは、提案されたデータ形式を指定する[**KSDATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)を返します。

Pin を提案されたデータ形式にリセットできる場合、KS フィルターは STATUS\_SUCCESS を返し、それ以外の場合はエラーコードを返します。 このプロパティ要求では、データ形式が変更されないことに注意してください。 クライアントは、 [**Ksk プロパティ\_接続\_DATAFORMAT**](ksproperty-connection-dataformat.md)を使用して形式を変更します。

「 [KS データ形式とデータ範囲](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-data-formats-and-data-ranges)」も参照してください。

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


[**KSK プロパティ\_接続\_DATAFORMAT**](ksproperty-connection-dataformat.md)

[*AVStrMiniPinSetDataFormat*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspinsetdataformat)

 

 






