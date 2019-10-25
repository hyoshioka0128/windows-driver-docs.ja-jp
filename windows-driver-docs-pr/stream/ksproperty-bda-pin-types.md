---
title: KSK プロパティ\_BDA\_PIN\_型
description: クライアントは、KSK プロパティ\_BDA\_ピン留め\_の種類を使用して、pin の種類の一覧を取得します。
ms.assetid: de11ab3c-a787-4831-aad4-e97f46432032
keywords:
- KSPROPERTY_BDA_PIN_TYPES ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_PIN_TYPES
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b2aee4de6cb7295202abc5b08ba34c0450a3b72e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838084"
---
# <a name="ksproperty_bda_pin_types"></a>KSK プロパティ\_BDA\_PIN\_型


クライアントは、KSK プロパティ\_BDA\_ピン留め\_の種類を使用して、pin の種類の一覧を取得します。

## <span id="ddk_ksproperty_bda_pin_types_ks"></span><span id="DDK_KSPROPERTY_BDA_PIN_TYPES_KS"></span>


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
<th>セット</th>
<th>的を絞る</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>はい</p></td>
<td><p>いいえ</p></td>
<td><p>filter</p></td>
<td><p>KSPROPERTY</p></td>
<td><p>KSPIN_DESCRIPTOR_EXs の一覧</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>解説
-------

テンプレートトポロジでは、各ピンの種類は1回しか実行できませんが、実際のトポロジでは複数回発生する可能性があります。 このピンの種類の一覧は、KSPIN\_記述子\_EX 構造体の配列です。

<a name="requirements"></a>前提条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>ヘッダー</p></td>
<td>Bdamedia (Bdamedia を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**BdaPropertyPinTypes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdapropertypintypes)

[**KSPIN\_記述子\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

 

 






