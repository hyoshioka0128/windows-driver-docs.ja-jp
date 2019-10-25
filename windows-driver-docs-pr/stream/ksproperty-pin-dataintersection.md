---
title: KSK プロパティ\_ピン\_DATAINTERSECTION 集合
description: クライアントは、KSK プロパティ\_ピン留め\_DATAINTERSECTION プロパティを使用して、pin ファクトリによってインスタンス化されたピンでサポートされるデータ形式を検索します。 クライアントは、データ形式の一覧を提供します。KS フィルターは、サポートされているリストの最初のデータ形式を返します。
ms.assetid: 447ac37b-1e5e-4812-9e1e-50e9f6f83118
keywords:
- KSPROPERTY_PIN_DATAINTERSECTION ストリーミングメディアデバイス
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
ms.openlocfilehash: a77145aa74df7f51f1d984c924f4cd542d1ee8e2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838860"
---
# <a name="ksproperty_pin_dataintersection"></a>KSK プロパティ\_ピン\_DATAINTERSECTION 集合


クライアントは、KSK プロパティ\_ピン留め\_DATAINTERSECTION プロパティを使用して、pin ファクトリによってインスタンス化されたピンでサポートされるデータ形式を検索します。 クライアントは、データ形式の一覧を提供します。KS フィルターは、サポートされているリストの最初のデータ形式を返します。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat" data-raw-source="[&lt;strong&gt;KSDATAFORMAT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)"><strong>KSDATAFORMAT</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

このプロパティを指定するには、 [**KSP\_ピン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)構造の後に[**ksk の複数\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)の構造体と、64ビットでアラインされた1つの[**ksmultiple**](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))体のシーケンスを指定します。 **KSP\_pin**の**pinid**メンバーは、pin ファクトリを指定します。

このプロパティは、クライアントが指定したリストから最初に一致したデータ形式を返します。

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

[**KSDATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)

 

 






