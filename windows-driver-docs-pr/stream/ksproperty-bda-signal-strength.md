---
title: KSK プロパティ\_BDA\_シグナル\_強度
description: クライアントは、KSK プロパティ\_BDA\_シグナル\_強度を使用して、mDb (1/1000/DB) の信号のキャリアの強さを決定します。
ms.assetid: b8b71135-cc0b-4a59-940a-dd766cab3305
keywords:
- KSPROPERTY_BDA_SIGNAL_STRENGTH ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_SIGNAL_STRENGTH
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01d9957d05a5d9b83b52a6a9732b3897d3013c26
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843604"
---
# <a name="ksproperty_bda_signal_strength"></a>KSK プロパティ\_BDA\_シグナル\_強度


クライアントは、KSK プロパティ\_BDA\_シグナル\_強度を使用して、mDb (1/1000/DB) の信号のキャリアの強さを決定します。

## <span id="ddk_ksproperty_bda_signal_strength_ks"></span><span id="DDK_KSPROPERTY_BDA_SIGNAL_STRENGTH_KS"></span>


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
<td><p>[はい]</p></td>
<td><p>ピン留めまたはフィルター</p></td>
<td><p>KSP_NODE</p></td>
<td><p>長い</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KSP の**NodeId**メンバー\_node は、コントロールノードの識別子を指定します。または、pin を指定するために−1に設定されています。

戻り値は、mDb の信号のキャリア強度を指定します。

指定された種類のブロードキャストネットワークでは、強度が0の場合は想定されている強度があります。 Subnominal の長所は、正の mDb として報告されます。 非常に名目上の長所は、否定 mDb として報告されます。

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
<td>Bdamedia (Bdamedia を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSP\_ノード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

 

 






