---
title: KSPROPERTY\_PIN\_DATARANGES
description: クライアントの使用、KSPROPERTY\_暗証番号 (pin)\_ピン pin ファクトリによってインスタンス化でサポートされているデータの範囲を判断する DATARANGES プロパティ。
ms.assetid: 90dd82c4-36a2-4fd3-b842-bbd9588a2740
keywords:
- KSPROPERTY_PIN_DATARANGES ストリーミング メディア デバイス
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
ms.openlocfilehash: 885de5eb6d8af481497d4de38873c61fa1019176
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393352"
---
# <a name="kspropertypindataranges"></a>KSPROPERTY\_PIN\_DATARANGES


クライアントの使用、KSPROPERTY\_暗証番号 (pin)\_ピン pin ファクトリによってインスタンス化でサポートされているデータの範囲を判断する DATARANGES プロパティ。

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
<td><p>A <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksmultiple_item" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksmultiple_item)"> <strong>KSMULTIPLE_ITEM</strong> </a>構造体、64 ビットの配置のシーケンスに続く<a href="https://docs.microsoft.com/previous-versions/ff561658(v=vs.85)" data-raw-source="[&lt;strong&gt;KSDATARANGE&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))"> <strong>KSDATARANGE</strong> </a>構造体。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

KSP を使用してこのプロパティを指定\_暗証番号 (pin)、場所、 **PinId**メンバーが許容可能なデータ範囲を返すためのファクトリを暗証番号 (pin) を指定します。

KS フィルターは、pin の pin ファクトリによってインスタンス化でサポートされているすべてのデータ範囲を返します。 KS フィルターは、現在の内部状態で報告されたデータ範囲をサポートしていません。 現在の内部状態でサポートされているデータの範囲を調べるには[ **KSPROPERTY\_PIN\_CONSTRAINEDDATARANGES**](ksproperty-pin-constraineddataranges.md)します。

Stream ミニドライバーは、このプロパティを直接処理する必要はありません。ストリーム クラス ドライバーは、ストリーム要求のブロックを使用して詳細情報を照会するこのプロパティを処理します。

詳細については、次を参照してください。 [KS データ形式とデータ範囲](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-data-formats-and-data-ranges)します。

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

[**KSMULTIPLE\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksmultiple_item)

[**KSDATARANGE**](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))

[**KSPROPERTY\_PIN\_CONSTRAINEDDATARANGES**](ksproperty-pin-constraineddataranges.md)

 

 






