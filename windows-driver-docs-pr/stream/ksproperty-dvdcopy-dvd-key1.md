---
title: KSPROPERTY\_DVDCOPY\_DVD\_[KEY1]
description: KSPROPERTY\_DVDCOPY\_DVD\_KEY1 プロパティをデコーダーに DVD 著作権保護の認証プロセスの一環として後で提供されている最初の bus キーを取得します。
ms.assetid: df4fd5a0-d890-4695-b8ec-951dd0e4e1d5
keywords:
- KSPROPERTY_DVDCOPY_DVD_KEY1 ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_DVDCOPY_DVD_KEY1
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3dae27734f18e5c0f3ea04c9e64e0753c650d64
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380630"
---
# <a name="kspropertydvdcopydvdkey1"></a>KSPROPERTY\_DVDCOPY\_DVD\_[KEY1]


KSPROPERTY\_DVDCOPY\_DVD\_KEY1 プロパティをデコーダーに DVD 著作権保護の認証プロセスの一環として後で提供されている最初の bus キーを取得します。

## <span id="ddk_ksproperty_dvdcopy_dvd_key1_ks"></span><span id="DDK_KSPROPERTY_DVDCOPY_DVD_KEY1_KS"></span>


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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567635" data-raw-source="[&lt;strong&gt;KS_DVDCOPY_BUSKEY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567635)"><strong>KS_DVDCOPY_BUSKEY</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、KS\_DVDCOPY\_DVD デコーダーの最初の bus キーを記述する BUSKEY 構造体。

<a name="remarks"></a>コメント
-------

最初のバス キーの詳細については、次を参照してください。 [DVD 著作権保護](https://msdn.microsoft.com/library/windows/hardware/ff558736)します。

<a name="requirements"></a>必要条件
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


[**KS\_DVDCOPY\_BUSKEY**](https://msdn.microsoft.com/library/windows/hardware/ff567635)

 

 






