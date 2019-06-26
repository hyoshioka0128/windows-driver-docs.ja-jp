---
title: KSPROPERTY\_PIN\_インターフェイス
description: このプロパティは、ピンのピン留めする特定のファクトリによってインスタンス化でサポートされているインターフェイスの一覧を返します。
ms.assetid: 5a49c685-d086-4827-87a3-67d1fa80452a
keywords:
- KSPROPERTY_PIN_INTERFACES ストリーミング メディア デバイス
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
ms.openlocfilehash: 61547c279e12b08076ff58f2cc22fd2081642268
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393331"
---
# <a name="kspropertypininterfaces"></a>KSPROPERTY\_PIN\_インターフェイス


このプロパティは、ピンのピン留めする特定のファクトリによってインスタンス化でサポートされているインターフェイスの一覧を返します。

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
<td><p>A <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksmultiple_item" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksmultiple_item)"> <strong>KSMULTIPLE_ITEM</strong> </a>のシーケンスに続く構造<a href="https://docs.microsoft.com/previous-versions/ff563537(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPIN_INTERFACE&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff563537(v=vs.85))"> <strong>KSPIN_INTERFACE</strong> </a>構造体。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KSPROPERTY 指定\_暗証番号 (pin)\_KSP を使用してインターフェイス\_暗証番号 (pin)、場所、 **PinId**メンバーが使用可能なインターフェイスを返すためのファクトリを暗証番号 (pin) を指定します。

このプロパティは、クラス ドライバーの優先順インターフェイスを返します。

Stream ミニドライバーは、このプロパティを直接処理する必要はありません。ストリーム クラス ドライバーは、ストリーム要求のブロックを使用して詳細情報を照会するこのプロパティを処理します。

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
<td>Ks.h (Ks.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSP\_暗証番号 (PIN)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_pin)

[**KSMULTIPLE\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksmultiple_item)

[**KSPIN\_インターフェイス**](https://docs.microsoft.com/previous-versions/ff563537(v=vs.85))

 

 






