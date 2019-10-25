---
title: KSK プロパティ\_BDA\_PIN\_ID
description: クライアントは、KSK プロパティ\_BDA\_ピン\_ID を使用して、pin の BDA 識別子 (ID) を取得します。
ms.assetid: 6f7a4454-1294-4646-8e21-bfec9a14b612
keywords:
- KSPROPERTY_BDA_PIN_ID ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_PIN_ID
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b7484e2541624da3e5677bb00a9c3e4f99791a5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837610"
---
# <a name="ksproperty_bda_pin_id"></a>KSK プロパティ\_BDA\_PIN\_ID


クライアントは、KSK プロパティ\_BDA\_ピン\_ID を使用して、pin の BDA 識別子 (ID) を取得します。

## <span id="ddk_ksproperty_bda_pin_id_ks"></span><span id="DDK_KSPROPERTY_BDA_PIN_ID_KS"></span>


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
<td><p>KSPROPERTY</p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

返される値は、pin ID を指定します。

ネットワークプロバイダーが KSK メソッドを使用してフィルターの pin を作成するときに\_BDA\_作成\_PIN\_ファクトリでは、フィルターの BDA ミニドライバーによって ID がピン留めされます。 KSK プロパティ\_BDA\_PIN\_ID は、この ID を返します。

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


[**KSK メソッド\_BDA\_作成\_PIN\_ファクトリ**](ksmethod-bda-create-pin-factory.md)

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

 

 






