---
title: KSPROPERTY\_VPCONFIG\_の構成
description: KSK プロパティ\_VPCONFIG\_"" は、ハードウェアによってビデオイメージのサイズを縮小できるかどうかを示します。
ms.assetid: a929b154-165e-4075-9295-d34fecc8e18d
keywords:
- KSPROPERTY_VPCONFIG_DECIMATIONCAPABILITY ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_VPCONFIG_DECIMATIONCAPABILITY
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae25af8099b552ceb95f7aa614b05b2da07af537
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842814"
---
# <a name="ksproperty_vpconfig_decimationcapability"></a>KSPROPERTY\_VPCONFIG\_の構成


KSK プロパティ\_VPCONFIG\_"" は、ハードウェアによってビデオイメージのサイズを縮小できるかどうかを示します。

## <span id="ddk_ksproperty_vpconfig_decimationcapability_ks"></span><span id="DDK_KSPROPERTY_VPCONFIG_DECIMATIONCAPABILITY_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p>Boolean</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) はブール値です。 ハードウェアがビデオイメージのサイズを縮小できる場合は**TRUE**を指定し、ハードウェアがサイズを縮小できない場合は **[FALSE]** を指定します。

<a name="remarks"></a>注釈
-------

プロパティ値が**TRUE の場合**、ビデオイメージのサイズを縮小できることを示します。 **FALSE**を指定すると、イメージのサイズを変更することはできますが、拡大縮小ではなく四角形にもクリップされます。

KSK プロパティ\_VPCONFIG\_\_、正常に完了したことを示す\_状態を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

このプロパティが KSPROPSETID\_VPVBIConfig によって使用されている場合、すべてのプロパティ要求は\_実装されていない状態\_返される必要があります。

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


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

 

 






