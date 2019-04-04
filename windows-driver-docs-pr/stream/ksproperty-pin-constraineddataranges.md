---
title: KSPROPERTY\_PIN\_CONSTRAINEDDATARANGES
description: KSPROPERTY\_PIN\_CONSTRAINEDDATARANGES プロパティが現在 pin の pin のファクトリでインスタンス化でサポートされてデータ範囲の一覧を指定します。
ms.assetid: 6328a128-c6f8-4de1-a86a-0a7c8a940e18
keywords:
- KSPROPERTY_PIN_CONSTRAINEDDATARANGES ストリーミング メディア デバイス
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
ms.openlocfilehash: e37fc6110a8d7be8f18df53d71c6e28b9caa97d1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557424"
---
# <a name="kspropertypinconstraineddataranges"></a>KSPROPERTY\_PIN\_CONSTRAINEDDATARANGES


KSPROPERTY\_PIN\_CONSTRAINEDDATARANGES プロパティが現在 pin の pin のファクトリでインスタンス化でサポートされてデータ範囲の一覧を指定します。

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
<td><p>Pin</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566722" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566722)"><strong>KSP_PIN</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff563441" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563441)"><strong>KSMULTIPLE_ITEM</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff561658" data-raw-source="[&lt;strong&gt;KSDATARANGE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561658)"> <strong>KSDATARANGE</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

**PinId**のメンバー、 [ **KSP\_PIN** ](https://msdn.microsoft.com/library/windows/hardware/ff566722)構造をクエリにピン留めするファクトリを指定します。

このプロパティを返します、 [ **KSMULTIPLE\_項目**](https://msdn.microsoft.com/library/windows/hardware/ff563441)構造体、64 ビットの配置のシーケンスに続く[ **KSDATARANGE** ](https://msdn.microsoft.com/library/windows/hardware/ff561658)構造体。

ピンをすべての制約に基づいてこの pin ファクトリでインスタンス化で現在サポートされているデータの範囲を報告するには、このプロパティは、KS フィルターの現在の内部状態によって課される KS フィルターの使用。 使用して、 [ **KSPROPERTY\_PIN\_DATARANGES** ](ksproperty-pin-dataranges.md)プロパティを動的な制約に関係なく、KS フィルターでサポートされているすべてのデータ範囲の完全な一覧を報告します。

Stream ミニドライバーは、このプロパティを直接処理する必要はありません。ストリーム クラス ドライバーは、ストリーム要求のブロックを使用して詳細情報を照会するこのプロパティを処理します。

詳細については、[KS データ形式とデータ範囲](https://msdn.microsoft.com/library/windows/hardware/ff567632)を参照してください。

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


[**KSMULTIPLE\_項目**](https://msdn.microsoft.com/library/windows/hardware/ff563441)

[**KSDATARANGE**](https://msdn.microsoft.com/library/windows/hardware/ff561658)

[**KSPROPERTY\_PIN\_DATARANGES**](ksproperty-pin-dataranges.md)

 

 






