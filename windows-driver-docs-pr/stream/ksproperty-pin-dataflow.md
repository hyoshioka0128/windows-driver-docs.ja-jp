---
title: KSPROPERTY\_PIN\_データ フロー
description: KSPROPERTY\_PIN\_データフロー プロパティ pin ファクトリによってインスタンス化するピンのデータ フローの方向を指定します。 シンクのピンは、フィルターのエントリ ポイントです。フィルターからソース ピンの出力。
ms.assetid: 3132b344-c4f3-48dc-9829-f4e97d0f18fc
keywords:
- KSPROPERTY_PIN_DATAFLOW ストリーミング メディア デバイス
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
ms.openlocfilehash: d1aeec825d25be1943ede5b9898156c3f264af05
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376659"
---
# <a name="kspropertypindataflow"></a>KSPROPERTY\_PIN\_データ フロー


KSPROPERTY\_PIN\_データフロー プロパティ pin ファクトリによってインスタンス化するピンのデータ フローの方向を指定します。 シンクのピンは、フィルターのエントリ ポイントです。フィルターからソース ピンの出力。

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
<th>取得</th>
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>〇</p></td>
<td><p>いいえ</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_pin" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_pin)"><strong>KSP_PIN</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ne-ks-kspin_dataflow" data-raw-source="[&lt;strong&gt;KSPIN_DATAFLOW&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ne-ks-kspin_dataflow)"><strong>KSPIN_DATAFLOW</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

ピン留めするファクトリを指定、 **PinId**のメンバー、 [ **KSP\_PIN** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_pin)構造体。

KSPROPERTY\_PIN\_データ フローは、型の列挙体を返します[ **KSPIN\_データフロー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ne-ks-kspin_dataflow)、いずれかに設定**KSPIN\_データ フロー\_IN**または KSPIN\_データフロー\_アウトします。

Stream ミニドライバーは、このプロパティを直接処理する必要はありません。ストリーム クラス ドライバーは、ストリーム要求のブロックを使用して詳細情報を照会するこのプロパティを処理します。

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
<td>Ks.h (Ks.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSP\_暗証番号 (PIN)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_pin)

[**KSPIN\_データ フロー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ne-ks-kspin_dataflow)

 

 






