---
title: KSK プロパティ\_ピン留め\_データフロー
description: KSK プロパティ\_ピン留め\_データフロープロパティは、ピンファクトリによってインスタンス化されるピンのデータフローの方向を指定します。 シンクピンはフィルターへのエントリポイントです。ソースピンはフィルターから出力します。
ms.assetid: 3132b344-c4f3-48dc-9829-f4e97d0f18fc
keywords:
- KSPROPERTY_PIN_DATAFLOW ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_PIN_DATAFLOW
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b4c64741903a733eb64bdf1fcc6e0c33c7c4d97
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838861"
---
# <a name="ksproperty_pin_dataflow"></a>KSK プロパティ\_ピン留め\_データフロー


KSK プロパティ\_ピン留め\_データフロープロパティは、ピンファクトリによってインスタンス化されるピンのデータフローの方向を指定します。 シンクピンはフィルターへのエントリポイントです。ソースピンはフィルターから出力します。

## <span id="ddk_ksproperty_pin_dataflow_ks"></span><span id="DDK_KSPROPERTY_PIN_DATAFLOW_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ne-ks-kspin_dataflow" data-raw-source="[&lt;strong&gt;KSPIN_DATAFLOW&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ne-ks-kspin_dataflow)"><strong>KSPIN_DATAFLOW</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

[**KSP\_pin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)構造体の**pinid**メンバーにピンファクトリを指定します。

KSK プロパティ\_ピン\_データフローでは、kspin [ **\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ne-ks-kspin_dataflow)データフローの列挙型が返されます。これは、または kspin\_データフロー\_OUT に **\_** 設定されます。

Stream ミニドライバーは、このプロパティを直接処理する必要はありません。ストリームクラスドライバーは、ストリーム要求ブロックを使用してこのプロパティを処理し、詳細情報を照会します。

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

[**KSPIN\_データフロー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ne-ks-kspin_dataflow)

 

 






