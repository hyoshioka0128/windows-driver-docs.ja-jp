---
title: KSK プロパティ\_アロケーター\_制御\_\_カウントを優先します
description: '\_アロケータープロパティは、アロケーター\_制御\_\_COUNT プロパティによって、割り当てられる DirectDraw サーフェイスの数を決定する方法をオーバーレイミキサーに通知します。 このプロパティは省略可能です。'
ms.assetid: 3a867554-a6ef-49bd-89e7-e5d09a21609e
keywords:
- KSPROPERTY_ALLOCATOR_CONTROL_HONOR_COUNT ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_ALLOCATOR_CONTROL_HONOR_COUNT
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04b46f380766a59b4694872a7a02d0166299f206
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832003"
---
# <a name="ksproperty_allocator_control_honor_count"></a>KSK プロパティ\_アロケーター\_制御\_\_カウントを優先します


\_アロケータープロパティは、アロケーター\_制御\_\_COUNT プロパティによって、割り当てられる DirectDraw サーフェイスの数を決定する方法をオーバーレイミキサーに通知します。 このプロパティは省略可能です。

## <span id="ddk_ksproperty_allocator_control_honor_count_ks"></span><span id="DDK_KSPROPERTY_ALLOCATOR_CONTROL_HONOR_COUNT_KS"></span>


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
<td><p>DWORD</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、オーバーレイの表面の数を計算するオーバーレイミキサーの方法を指定する DWORD です。

<a name="remarks"></a>注釈
-------

KSK プロパティ\_アロケーター\_制御\_を優先\_COUNT プロパティ要求は1を返す必要があります。オーバーレイミキサーが Ksk プロパティで指定されたサーフェイスの数を強制的に使用するようにするには、 [**ALLOCATORFRAMING\_接続\_** ](ksproperty-connection-allocatorframing.md)". 戻り値が0の場合、オーバーレイミキサーによって、割り当てられるサーフェイスの数が計算されます。

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
<td>Ksmedia .h (Ksk を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSK プロパティ\_接続\_ALLOCATORFRAMING**](ksproperty-connection-allocatorframing.md)

 

 






