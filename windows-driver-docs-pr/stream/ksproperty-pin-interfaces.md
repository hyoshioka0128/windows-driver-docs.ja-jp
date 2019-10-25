---
title: KSK プロパティ\_ピン留め\_インターフェイス
description: このプロパティは、特定のピンファクトリによってインスタンス化されたピンでサポートされるインターフェイスの一覧を返します。
ms.assetid: 5a49c685-d086-4827-87a3-67d1fa80452a
keywords:
- KSPROPERTY_PIN_INTERFACES ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_PIN_INTERFACES
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a5fa4a72e0583e3effcbd6e32db62a0b8a6eb08
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838849"
---
# <a name="ksproperty_pin_interfaces"></a>KSK プロパティ\_ピン留め\_インターフェイス


このプロパティは、特定のピンファクトリによってインスタンス化されたピンでサポートされるインターフェイスの一覧を返します。

## <span id="ddk_ksproperty_pin_interfaces_ks"></span><span id="DDK_KSPROPERTY_PIN_INTERFACES_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)"><strong>KSMULTIPLE_ITEM</strong></a>構造体の後に、一連の<a href="https://docs.microsoft.com/previous-versions/ff563537(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPIN_INTERFACE&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff563537(v=vs.85))"><strong>KSPIN_INTERFACE</strong></a>構造体。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

\_KSK プロパティを指定します。 KSP\_ピンを使用して\_インターフェイスをピン留めします。この場合、 **Pinid**メンバーは、使用可能なインターフェイスを返すための pin ファクトリを指定します。

このプロパティは、クラスドライバーの優先順位によって順序付けられたインターフェイスを返します。

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

[**KSPIN\_インターフェイス**](https://docs.microsoft.com/previous-versions/ff563537(v=vs.85))

 

 






