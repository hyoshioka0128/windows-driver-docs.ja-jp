---
title: KSK プロパティ\_ストリーム\_の劣化
description: KSK プロパティ\_STREAM\_劣化プロパティはオプションのプロパティであり、pin によって劣化戦略が可能な場合に実装する必要があります。
ms.assetid: b8f9db81-a9ed-4a13-8d64-14854193c91b
keywords:
- KSPROPERTY_STREAM_DEGRADATION ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_STREAM_DEGRADATION
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: cfc104f7b61d032819b75fd434b2128684414b09
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844957"
---
# <a name="ksproperty_stream_degradation"></a>KSK プロパティ\_ストリーム\_の劣化


KSK プロパティ\_STREAM\_劣化プロパティはオプションのプロパティであり、pin によって劣化戦略が可能な場合に実装する必要があります。

## <span id="ddk_ksproperty_stream_degradation_ks"></span><span id="DDK_KSPROPERTY_STREAM_DEGRADATION_KS"></span>


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
<td><p>[はい]</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)"><strong>KSMULTIPLE_ITEM</strong></a>、 <a href="https://docs.microsoft.com/previous-versions/ff561671(v=vs.85)" data-raw-source="[&lt;strong&gt;KSDEGRADE&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff561671(v=vs.85))"> <strong>KSDEGRADE</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

クエリを行うと、プロパティは、 [**Ksmultiple\_ITEM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)形式で返される構造体のサイズと数を返し、その後に[**ksmultiple**](https://docs.microsoft.com/previous-versions/ff561671(v=vs.85))構造体を低下させます。

クエリでは、このプロパティは、KSMULTIPLE\_ITEM 形式で返される構造体のサイズと数を返し、その後に KSK を使用する構造体を返します。 複数の項目の形式は、クエリと設定の低下戦略の両方で使用する必要があります。

クライアントはこのプロパティを照会して現在の低下設定を取得できます。また、このプロパティを設定して、現在の低下設定を変更することもできます。 パフォーマンス低下の設定は、品質管理 (QM) への応答としてフィルターの pin によってリソースの使用量を変更する場合、または品質をさらに高いレベルに調整する場合に使用します。 これは通常、品質管理者が低下設定を調整し、調整可能な設定の種類とその現在の値を照会するために使用されます。 値を設定するときに、複数の KSDEGRADE する構造体を渡すことができます。 品質マネージャーの詳細については、「 [Quality Management](https://docs.microsoft.com/windows-hardware/drivers/stream/quality-management)」を参照してください。

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


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSMULTIPLE\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)

[**KSDEGRADE**](https://docs.microsoft.com/previous-versions/ff561671(v=vs.85))

 

 






