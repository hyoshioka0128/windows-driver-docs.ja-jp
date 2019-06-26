---
title: KSPROPERTY\_BDA\_PIN\_型
description: クライアントを使用して、KSPROPERTY\_BDA\_PIN\_暗証番号 (pin) の種類を示す値を取得する型。
ms.assetid: 3d2a976b-67ff-4469-aa96-7aa8bd5f229e
keywords:
- KSPROPERTY_BDA_PIN_TYPE ストリーミング メディア デバイス
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
ms.openlocfilehash: 7a2a06f0bbd9dc88698a61242966e3263c29e8b5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368134"
---
# <a name="kspropertybdapintype"></a>KSPROPERTY\_BDA\_PIN\_型


クライアントを使用して、KSPROPERTY\_BDA\_PIN\_暗証番号 (pin) の種類を示す値を取得する型。

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
<td><p>KSPROPERTY</p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

返される値は、暗証番号 (pin) の種類を指定します。

ネットワーク プロバイダーが KSMETHOD を使用してフィルターの暗証番号 (pin) を作成するときに\_BDA\_作成\_PIN\_ファクトリ、フィルターの BDA テンプレートのトポロジに含まれる暗証番号 (pin) の種類の一覧からの暗証番号 (pin) 型を指定します。 KSPROPERTY\_BDA\_PIN\_型は、このピンの型を返します。 BDA テンプレート トポロジでは、フィルターの各ピンの型は 1 回だけが実際のトポロジで複数回が発生することができます。 暗証番号 (pin) の型の値は、暗証番号 (pin) の型の 0 から始まる配列内の要素のインデックスに対応します。 このピンの型の配列は配列 KSPIN の\_記述子\_EX 構造体。

<a name="requirements"></a>必要条件
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


[**KSMETHOD\_BDA\_作成\_PIN\_ファクトリ**](ksmethod-bda-create-pin-factory.md)

[**KSPIN\_記述子\_例**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin_descriptor_ex)

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

 

 






