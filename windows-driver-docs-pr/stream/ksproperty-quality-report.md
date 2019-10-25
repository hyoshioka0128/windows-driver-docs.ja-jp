---
title: KSK プロパティ\_品質\_レポート
description: KSK プロパティ\_QUALITY\_REPORT プロパティは、pin が品質管理をサポートしている場合に実装する必要があるオプションのプロパティです。
ms.assetid: 9879a28d-aa92-4583-be63-03fed67c8416
keywords:
- KSPROPERTY_QUALITY_REPORT ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_QUALITY_REPORT
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e6cda26b7e36845fba333d601a49c5104bc18aac
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838833"
---
# <a name="ksproperty_quality_report"></a>KSK プロパティ\_品質\_レポート


KSK プロパティ\_QUALITY\_REPORT プロパティは、pin が品質管理をサポートしている場合に実装する必要があるオプションのプロパティです。

## <span id="ddk_ksproperty_quality_report_ks"></span><span id="DDK_KSPROPERTY_QUALITY_REPORT_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksquality" data-raw-source="[&lt;strong&gt;KSQUALITY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksquality)"><strong>KSK 品質</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KSK プロパティ\_品質\_レポートには、 [**Ksk 品質**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksquality)構造型のプロパティ値があります。 この構造体を使用して、現在使用されているフレームの割合と、最適なフレームの受信時刻からのデルタを取得または設定します。

クラスドライバーは、このプロパティを処理しません。stream ミニドライバーは、独自の処理を提供する必要があります。

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

[**KSK 品質**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksquality)

 

 






