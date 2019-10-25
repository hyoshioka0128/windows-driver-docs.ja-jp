---
title: KSK プロパティ\_PIN\_DATARANGES
description: クライアントは、KSK プロパティ\_ピン留め\_DATARANGES プロパティを使用して、pin ファクトリによってインスタンス化されたピンによってサポートされるデータ範囲を決定します。
ms.assetid: 90dd82c4-36a2-4fd3-b842-bbd9588a2740
keywords:
- KSPROPERTY_PIN_DATARANGES ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_PIN_DATARANGES
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 755fd0864fd23d9d22bb0d73049e7f6e02b28b4d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838857"
---
# <a name="ksproperty_pin_dataranges"></a>KSK プロパティ\_PIN\_DATARANGES


クライアントは、KSK プロパティ\_ピン留め\_DATARANGES プロパティを使用して、pin ファクトリによってインスタンス化されたピンによってサポートされるデータ範囲を決定します。

## <span id="ddk_ksproperty_pin_dataranges_ks"></span><span id="DDK_KSPROPERTY_PIN_DATARANGES_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)"><strong>KSMULTIPLE_ITEM</strong></a>構造体の後に、一連の64ビットアラインされた<a href="https://docs.microsoft.com/previous-versions/ff561658(v=vs.85)" data-raw-source="[&lt;strong&gt;KSDATARANGE&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))"><strong>ksk</strong></a>の構造体。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

このプロパティは、KSP\_PIN を使用して指定します。この場合、 **Pinid**メンバーは、受け入れ可能なデータ範囲を返す pin ファクトリを指定します。

KS フィルターは、ピンファクトリによってインスタンス化されたピンでサポートされるすべてのデータ範囲を返します。 KS フィルターは、現在の内部状態で報告されたデータ範囲をサポートしていない可能性があります。 現在の内部状態でサポートされているデータ範囲を確認するには、 [**Ksk プロパティ\_\_CONSTRAINEDDATARANGES**](ksproperty-pin-constraineddataranges.md)を使用します。

Stream ミニドライバーは、このプロパティを直接処理する必要はありません。ストリームクラスドライバーは、ストリーム要求ブロックを使用してこのプロパティを処理し、詳細情報を照会します。

詳細については、「 [KS データ形式とデータ範囲](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-data-formats-and-data-ranges)」を参照してください。

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

[**KSDATARANGE 場合**](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))

[**KSK プロパティ\_PIN\_CONSTRAINEDDATARANGES**](ksproperty-pin-constraineddataranges.md)

 

 






