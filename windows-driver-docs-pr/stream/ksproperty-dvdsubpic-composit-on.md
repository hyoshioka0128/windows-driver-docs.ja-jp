---
title: KSPROPERTY\_DVDSUBPIC\_に\_
description: KSK プロパティ\_DVDSUBPIC\_に\_プロパティは、サブピクチャの表示を有効または無効にします。
ms.assetid: f9dcf8ca-44fb-45e2-9993-813439c742ef
keywords:
- KSPROPERTY_DVDSUBPIC_COMPOSIT_ON ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_DVDSUBPIC_COMPOSIT_ON
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 65352100f3998f77d4a9c70e637d3649d155d59c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827119"
---
# <a name="ksproperty_dvdsubpic_composit_on"></a>KSPROPERTY\_DVDSUBPIC\_に\_


KSK プロパティ\_DVDSUBPIC\_に\_プロパティは、サブピクチャの表示を有効または無効にします。

## <span id="ddk_ksproperty_dvdsubpic_composit_on_ks"></span><span id="DDK_KSPROPERTY_DVDSUBPIC_COMPOSIT_ON_KS"></span>


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
<td><p>KSPROPERTY_COMPOSIT_ON</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、\_オン (型定義のブール値)\_の KSK プロパティです。 サブピクチャ表示を有効にする**場合は TRUE**を指定します。サブピクチャ表示を無効にする場合は**FALSE**を指定します。

<a name="remarks"></a>注釈
-------

サブピクチャ表示が無効になっている場合でも、デコーダーはサブピクチャデータをデコードする必要がありますが、表示はされません。 これにより、サブピクチャ有効化コマンドを受信したときに瞬時に表示されるようになります。

サブピクチャデータコマンドストリームには、プロパティ\_DVDSUBPIC\_\_の KSK プロパティをオーバーライドできる強制表示サブピクチャコマンドがあります。

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

 

 





