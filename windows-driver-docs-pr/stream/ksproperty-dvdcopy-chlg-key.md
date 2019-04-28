---
title: KSPROPERTY\_DVDCOPY\_CHLG\_キー
description: KSPROPERTY\_DVDCOPY\_CHLG\_キー プロパティは、DVD デコーダーと DVD ドライブを提供するバス チャレンジ キーを転送します。
ms.assetid: 744ea965-29dc-401f-8f68-7d63b58b6151
keywords:
- KSPROPERTY_DVDCOPY_CHLG_KEY ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_DVDCOPY_CHLG_KEY
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37c409bc89a4bda598119b083e659601e4623c61
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380639"
---
# <a name="kspropertydvdcopychlgkey"></a>KSPROPERTY\_DVDCOPY\_CHLG\_キー


KSPROPERTY\_DVDCOPY\_CHLG\_キー プロパティは、DVD デコーダーと DVD ドライブを提供するバス チャレンジ キーを転送します。

## <span id="ddk_ksproperty_dvdcopy_chlg_key_ks"></span><span id="DDK_KSPROPERTY_DVDCOPY_CHLG_KEY_KS"></span>


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
<td><p>〇</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567636" data-raw-source="[&lt;strong&gt;KS_DVDCOPY_CHLGKEY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567636)"><strong>KS_DVDCOPY_CHLGKEY</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、KS\_DVDCOPY\_bus チャレンジのキーを記述する CHLGKEY 構造体。

<a name="remarks"></a>注釈
-------

**取得**要求すると、DVD デコーダーがそのバス チャレンジのキーを提供します。 **設定**要求すると、DVD デコーダーが DVD ドライブから bus チャレンジのキーを提供します。

バスの課題のキーの詳細については、次を参照してください。 [DVD 著作権保護](https://msdn.microsoft.com/library/windows/hardware/ff558736)します。

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

## <a name="see-also"></a>関連項目


[**KS\_DVDCOPY\_CHLGKEY**](https://msdn.microsoft.com/library/windows/hardware/ff567636)

 

 






