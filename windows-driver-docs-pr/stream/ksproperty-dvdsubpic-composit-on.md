---
title: KSPROPERTY\_DVDSUBPIC\_複合\_ON
description: KSPROPERTY\_DVDSUBPIC\_複合\_プロパティで有効にまたはサブピクチャの表示を無効にします。
ms.assetid: f9dcf8ca-44fb-45e2-9993-813439c742ef
keywords:
- KSPROPERTY_DVDSUBPIC_COMPOSIT_ON ストリーミング メディア デバイス
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
ms.openlocfilehash: ad7c137a9059ab600eec0ccbff32b06d8445ffc3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529984"
---
# <a name="kspropertydvdsubpiccompositon"></a>KSPROPERTY\_DVDSUBPIC\_複合\_ON


KSPROPERTY\_DVDSUBPIC\_複合\_プロパティで有効にまたはサブピクチャの表示を無効にします。

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
<th>取得</th>
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>X</p></td>
<td><p>〇</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p>KSPROPERTY_COMPOSIT_ON</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、KSPROPERTY\_複合\_(型定義 Boolean) にします。 指定**TRUE**サブピクチャ表示を有効にするかを指定する**FALSE**サブピクチャ表示をオフにします。

<a name="remarks"></a>注釈
-------

サブピクチャ表示が無効になっている場合、デコーダーする必要がありますサブピクチャ データにまだデコードしますが、表示されません。 サブピクチャ-有効にするコマンドが受信したときに、インスタント表示が容易にします。

Force 表示サブピクチャ コマンド、KSPROPERTY をオーバーライドできるサブピクチャ データ コマンド ストリーム内でが\_DVDSUBPIC\_複合\_プロパティ。

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
<td>Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

 

 





