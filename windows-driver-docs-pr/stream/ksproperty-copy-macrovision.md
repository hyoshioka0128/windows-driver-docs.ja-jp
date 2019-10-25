---
title: KSK プロパティ\_コピー\_MACROVISION
description: KSK プロパティ\_COPY\_MACROVISION プロパティは、データストリームの Macrovision レベルを示します。
ms.assetid: 6863bcf6-06bc-4bd2-896e-43c083aa07d5
keywords:
- KSPROPERTY_COPY_MACROVISION ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_COPY_MACROVISION
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc20a81b063e1680f9fc701776720a7baa3aaafe
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826773"
---
# <a name="ksproperty_copy_macrovision"></a>KSK プロパティ\_コピー\_MACROVISION


KSK プロパティ\_COPY\_MACROVISION プロパティは、データストリームの Macrovision レベルを示します。

## <span id="ddk_ksproperty_copy_macrovision_ks"></span><span id="DDK_KSPROPERTY_COPY_MACROVISION_KS"></span>


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
<td><p>必須ではない</p></td>
<td><p>[はい]</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_copy_macrovision" data-raw-source="[&lt;strong&gt;KS_COPY_MACROVISION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_copy_macrovision)"><strong>KS_COPY_MACROVISION</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は\_\_MACROVISION 構造体で、データストリームの Macrovision レベルを指定します。

<a name="remarks"></a>注釈
-------

Macrovision レベルの詳細については、「 [DVD Copyright Protection](https://docs.microsoft.com/windows-hardware/drivers/stream/dvd-copyright-protection)」を参照してください。

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
<td>Ksmedia .h (Ksk を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KS\_コピー\_MACROVISION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_copy_macrovision)

 

 






