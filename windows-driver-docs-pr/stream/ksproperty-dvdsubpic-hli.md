---
title: KSK プロパティ\_DVDSUBPIC\_HLI
description: KSK プロパティ\_DVDSUBPIC\_HLI プロパティは、色やコントラストなど、変更するサブピクチャまたは画面の四角形を指定します。
ms.assetid: c3498ff8-11fe-4f53-8317-83a487684ac7
keywords:
- KSPROPERTY_DVDSUBPIC_HLI ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_DVDSUBPIC_HLI
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b2eb82b02be16ddddfdfdf08b4473c133108f1eb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827082"
---
# <a name="ksproperty_dvdsubpic_hli"></a>KSK プロパティ\_DVDSUBPIC\_HLI


KSK プロパティ\_DVDSUBPIC\_HLI プロパティは、色やコントラストなど、変更するサブピクチャまたは画面の四角形を指定します。

## <span id="ddk_ksproperty_dvdsubpic_hli_ks"></span><span id="DDK_KSPROPERTY_DVDSUBPIC_HLI_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksproperty_sphli" data-raw-source="[&lt;strong&gt;KSPROPERTY_SPHLI&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksproperty_sphli)"><strong>KSPROPERTY_SPHLI</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、変更する DVD の強調表示情報を記述する KSK プロパティ\_SPHLI 構造体です。

<a name="remarks"></a>注釈
-------

[**Ksk プロパティ\_SPHLI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksproperty_sphli)構造体は、DVD の強調表示情報から現在選択されているボタンを記述します。

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


[**KSK プロパティ\_SPHLI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksproperty_sphli)

 

 






