---
title: KSK プロパティ\_PIN\_NECESSARYINSTANCES
description: このプロパティは、フィルターが i/o 操作を実行する前に、ピンファクトリがインスタンス化する必要がある pin の最小数を返します。
ms.assetid: d30d7546-3d16-42df-b640-a8ec37bca35c
keywords:
- KSPROPERTY_PIN_NECESSARYINSTANCES ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_PIN_NECESSARYINSTANCES
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: df8aaa3d643d9567117102b3dba60ee27c3d4b85
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838848"
---
# <a name="ksproperty_pin_necessaryinstances"></a>KSK プロパティ\_PIN\_NECESSARYINSTANCES


このプロパティは、フィルターが i/o 操作を実行する前に、ピンファクトリがインスタンス化する必要がある pin の最小数を返します。

## <span id="ddk_ksproperty_pin_necessaryinstances_ks"></span><span id="DDK_KSPROPERTY_PIN_NECESSARYINSTANCES_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)"><strong>KSP_PIN</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

このプロパティは、KSP\_PIN を使用して指定します。この場合、メンバーは関連するピンファクトリを指定します。

KSK プロパティ\_PIN\_NECESSARYINSTANCES は、ピンファクトリがインスタンス化する必要のある pin の最小数を指定して、ULONG 型の値を返します。

クラスドライバーは、このプロパティを処理しません。stream ミニドライバーは、独自の処理を提供する必要があります。

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


[**KSP\_ピン留め**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)

 

 






