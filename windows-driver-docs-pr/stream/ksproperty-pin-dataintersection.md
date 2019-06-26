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
ms.openlocfilehash: 79e4fceeed8bffeccb34b3605b57231eb2ec11e9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371152"
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
<td><p>いいえ</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_pin" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_pin)"><strong>KSP_PIN</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksdataformat" data-raw-source="[&lt;strong&gt;KSDATAFORMAT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksdataformat)"><strong>KSDATAFORMAT</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

このプロパティを指定するには、提供、 [ **KSP\_PIN** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_pin)構造が続く、 [ **KSMULTIPLE\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksmultiple_item)構造体と 64 ビットのシーケンスに不整合[ **KSDATARANGE** ](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))構造体。 **PinId**のメンバー **KSP\_PIN**暗証番号 (pin) ファクトリを指定します。

このプロパティは、クライアントが指定したリストから、最初の一致するデータ形式を返します。

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

[**KSDATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksdataformat)

 

 






