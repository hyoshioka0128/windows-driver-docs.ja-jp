---
title: KSK プロパティ\_BDA\_PIN\_型
description: クライアントは、KSK プロパティ\_BDA\_\_PIN の種類を指定する値を取得するために使用します。
ms.assetid: 3d2a976b-67ff-4469-aa96-7aa8bd5f229e
keywords:
- KSPROPERTY_BDA_PIN_TYPE ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_PIN_TYPE
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8b2db83db07dc62fc1db06d8a65e653852a8759
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827456"
---
# <a name="ksproperty_bda_pin_type"></a>KSK プロパティ\_BDA\_PIN\_型


クライアントは、KSK プロパティ\_BDA\_\_PIN の種類を指定する値を取得するために使用します。

## <span id="ddk_ksproperty_bda_pin_type_ks"></span><span id="DDK_KSPROPERTY_BDA_PIN_TYPE_KS"></span>


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

戻り値は、pin の種類を指定します。

ネットワークプロバイダーが KSK メソッドを使用してフィルターの pin を作成し\_BDA\_作成\_PIN\_ファクトリでは、フィルターの BDA テンプレートトポロジに含まれる pin の種類の一覧から pin の種類を指定します。 KSK プロパティ\_BDA\_PIN\_型は、この pin の種類を返します。 フィルターの BDA テンプレートトポロジでは、各ピンの種類は1回しか実行できませんが、実際のトポロジでは複数回発生する可能性があります。 ピンの種類の値は、ピンの種類の0から始まる配列内の要素のインデックスに対応します。 このピンの種類の配列は、KSPIN\_記述子\_EX 構造体の配列です。

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

[**KSPIN\_記述子\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

 

 






