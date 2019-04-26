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
ms.openlocfilehash: 7af2687bab3f03764921a78428f4cf800f86ec13
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346385"
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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566722" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566722)"><strong>KSP_PIN</strong></a></p></td>
<td><p>A <a href="https://msdn.microsoft.com/library/windows/hardware/ff563441" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563441)"> <strong>KSMULTIPLE_ITEM</strong> </a>構造体、64 ビットの配置のシーケンスに続く<a href="https://msdn.microsoft.com/library/windows/hardware/ff561658" data-raw-source="[&lt;strong&gt;KSDATARANGE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561658)"> <strong>KSDATARANGE</strong> </a>構造体。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

KSP を使用してこのプロパティを指定\_暗証番号 (pin)、場所、 **PinId**メンバーが許容可能なデータ範囲を返すためのファクトリを暗証番号 (pin) を指定します。

KS フィルターは、pin の pin ファクトリによってインスタンス化でサポートされているすべてのデータ範囲を返します。 KS フィルターは、現在の内部状態で報告されたデータ範囲をサポートしていません。 現在の内部状態でサポートされているデータの範囲を調べるには[ **KSPROPERTY\_PIN\_CONSTRAINEDDATARANGES**](ksproperty-pin-constraineddataranges.md)します。

Stream ミニドライバーは、このプロパティを直接処理する必要はありません。ストリーム クラス ドライバーは、ストリーム要求のブロックを使用して詳細情報を照会するこのプロパティを処理します。

詳細については、次を参照してください。 [KS データ形式とデータ範囲](https://msdn.microsoft.com/library/windows/hardware/ff567632)します。

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


[**KSP\_暗証番号 (PIN)**](https://msdn.microsoft.com/library/windows/hardware/ff566722)

[**KSMULTIPLE\_項目**](https://msdn.microsoft.com/library/windows/hardware/ff563441)

[**KSDATARANGE**](https://msdn.microsoft.com/library/windows/hardware/ff561658)

[**KSPROPERTY\_PIN\_CONSTRAINEDDATARANGES**](ksproperty-pin-constraineddataranges.md)

 

 






