---
title: KSK プロパティ\_ピン\_メディア
description: このプロパティは、特定のピンファクトリによってインスタンス化されたピンでサポートされているメディアの一覧を返します。
ms.assetid: e92c7a3d-4f72-4818-9a26-0e82c20bdb4c
keywords:
- KSPROPERTY_PIN_MEDIUMS ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_PIN_MEDIUMS
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 102be0ada2319573ec1f999581ee9660b9d423c1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838854"
---
# <a name="ksproperty_pin_mediums"></a>KSK プロパティ\_ピン\_メディア


このプロパティは、特定のピンファクトリによってインスタンス化されたピンでサポートされているメディアの一覧を返します。

## <span id="ddk_ksproperty_pin_mediums_ks"></span><span id="DDK_KSPROPERTY_PIN_MEDIUMS_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)"><strong>KSMULTIPLE_ITEM</strong></a>構造体の後に、一連の<a href="https://docs.microsoft.com/previous-versions/ff563538(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPIN_MEDIUM&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff563538(v=vs.85))"><strong>KSPIN_MEDIUM</strong></a>構造体。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

クライアントは、このプロパティを使用して、pin ファクトリによってインスタンス化された pin によってサポートされるすべてのメディアの一覧を要求します。 クライアントは、pin に接続するときに使用する実際のメディアを指定します。

このプロパティは、KSP\_PIN を使用して指定します。この場合、メンバーは、メディアの一覧を返すピンファクトリを指定します。

KSK プロパティ\_PIN\_メディアは、クラスドライバーの優先順位に従ってメディアを返します。

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

[**KSMULTIPLE\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)

[**KSPIN\_中**](https://docs.microsoft.com/previous-versions/ff563538(v=vs.85))

 

 






