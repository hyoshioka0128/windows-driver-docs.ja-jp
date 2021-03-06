---
title: KSPROPERTY\_BDA\_PIN\_型
description: クライアントを使用して、KSPROPERTY\_BDA\_PIN\_暗証番号 (pin) の種類の一覧を取得する型。
ms.assetid: de11ab3c-a787-4831-aad4-e97f46432032
keywords:
- KSPROPERTY_BDA_PIN_TYPES ストリーミング メディア デバイス
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
ms.openlocfilehash: 9bad1b911e3a2210cf964163b307fb766e94382a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368122"
---
# <a name="kspropertybdapintypes"></a>KSPROPERTY\_BDA\_PIN\_型


クライアントを使用して、KSPROPERTY\_BDA\_PIN\_暗証番号 (pin) の種類の一覧を取得する型。

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
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>〇</p></td>
<td><p>X</p></td>
<td><p>フィルター</p></td>
<td><p>KSPROPERTY</p></td>
<td><p>KSPIN_DESCRIPTOR_EXs の一覧</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

テンプレートのトポロジで各種のピン留めすることができます 1 回だけが、実際のトポロジで複数回が発生する可能性が。 このピンの種類の一覧が KSPIN の配列\_記述子\_EX 構造体。

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
<td>Bdamedia.h (Bdamedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**BdaPropertyPinTypes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bdasup/nf-bdasup-bdapropertypintypes)

[**KSPIN\_記述子\_例**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin_descriptor_ex)

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

 

 






