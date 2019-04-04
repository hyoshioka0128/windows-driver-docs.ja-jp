---
title: KSPROPERTY\_PIN\_DATAINTERSECTION
description: クライアントの使用、KSPROPERTY\_PIN\_ピン pin ファクトリによってインスタンス化でサポートされるデータ形式を検索する DATAINTERSECTION プロパティ。 クライアントが別のデータ形式の一覧を提供します。KS フィルターは、サポートされている一覧の最初のデータ形式を返します。
ms.assetid: 447ac37b-1e5e-4812-9e1e-50e9f6f83118
keywords:
- KSPROPERTY_PIN_DATAINTERSECTION ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_PIN_DATAINTERSECTION
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0a57c7c3eba65539a9296009826b900a81da3b5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559478"
---
# <a name="kspropertypindataintersection"></a>KSPROPERTY\_PIN\_DATAINTERSECTION


クライアントの使用、KSPROPERTY\_PIN\_ピン pin ファクトリによってインスタンス化でサポートされるデータ形式を検索する DATAINTERSECTION プロパティ。 クライアントが別のデータ形式の一覧を提供します。KS フィルターは、サポートされている一覧の最初のデータ形式を返します。

## <span id="ddk_ksproperty_pin_dataintersection_ks"></span><span id="DDK_KSPROPERTY_PIN_DATAINTERSECTION_KS"></span>


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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561656" data-raw-source="[&lt;strong&gt;KSDATAFORMAT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561656)"><strong>KSDATAFORMAT</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

このプロパティを指定するには、提供、 [ **KSP\_PIN** ](https://msdn.microsoft.com/library/windows/hardware/ff566722)構造が続く、 [ **KSMULTIPLE\_項目**](https://msdn.microsoft.com/library/windows/hardware/ff563441)構造体と 64 ビットのシーケンスに不整合[ **KSDATARANGE** ](https://msdn.microsoft.com/library/windows/hardware/ff561658)構造体。 **PinId**のメンバー **KSP\_PIN**暗証番号 (pin) ファクトリを指定します。

このプロパティは、クライアントが指定したリストから、最初の一致するデータ形式を返します。

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


[**KSP\_暗証番号 (PIN)**](https://msdn.microsoft.com/library/windows/hardware/ff566722)

[**KSMULTIPLE\_項目**](https://msdn.microsoft.com/library/windows/hardware/ff563441)

[**KSDATARANGE**](https://msdn.microsoft.com/library/windows/hardware/ff561658)

[**KSDATAFORMAT**](https://msdn.microsoft.com/library/windows/hardware/ff561656)

 

 






