---
title: KSK プロパティ\_PIN\_CONSTRAINEDDATARANGES
description: KSK プロパティ\_PIN\_CONSTRAINEDDATARANGES プロパティは、pin ファクトリでインスタンス化されたピンで現在サポートされているデータ範囲のリストを指定します。
ms.assetid: 6328a128-c6f8-4de1-a86a-0a7c8a940e18
keywords:
- KSPROPERTY_PIN_CONSTRAINEDDATARANGES ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_PIN_CONSTRAINEDDATARANGES
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: de488f35e091aada637db5c1d71ae293fbb77164
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842751"
---
# <a name="ksproperty_pin_constraineddataranges"></a>KSK プロパティ\_PIN\_CONSTRAINEDDATARANGES


KSK プロパティ\_PIN\_CONSTRAINEDDATARANGES プロパティは、pin ファクトリでインスタンス化されたピンで現在サポートされているデータ範囲のリストを指定します。

## <span id="ddk_ksproperty_pin_constraineddataranges_ks"></span><span id="DDK_KSPROPERTY_PIN_CONSTRAINEDDATARANGES_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)"><strong>KSMULTIPLE_ITEM</strong></a>と<a href="https://docs.microsoft.com/previous-versions/ff561658(v=vs.85)" data-raw-source="[&lt;strong&gt;KSDATARANGE&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))"> <strong>ksdatarange</strong>場合</a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

[**KSP\_ピン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)構造の**pinid**メンバーは、クエリを実行するための pin ファクトリを指定します。

このプロパティは、 [**Ksmultiple\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)の構造体を返し、その後に一連の64ビットアラインされた[**ksk**](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))の構造体を返します。

KS フィルターでは、このプロパティを使用して、KS フィルターの現在の内部状態によって課される制約に基づいて、このピンファクトリでインスタンス化されたピンで現在サポートされているデータ範囲を報告します。 動的制約にかかわらず、DATARANGES プロパティを使用して、KS フィルターでサポートされているすべてのデータ範囲の完全な一覧を報告するには、 [**Ksk プロパティ\_\_** ](ksproperty-pin-dataranges.md)プロパティを使用します。

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


[**KSMULTIPLE\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)

[**KSDATARANGE 場合**](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))

[**KSK プロパティ\_PIN\_DATARANGES**](ksproperty-pin-dataranges.md)

 

 






