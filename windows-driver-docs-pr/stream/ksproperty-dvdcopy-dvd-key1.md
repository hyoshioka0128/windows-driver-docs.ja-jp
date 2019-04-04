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
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573350"
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
<th>Set</th>
<th>移行先</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>いいえ</p></td>
<td><p>はい</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567635" data-raw-source="[&lt;strong&gt;KS_DVDCOPY_BUSKEY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567635)"><strong>KS_DVDCOPY_BUSKEY</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、KS\_DVDCOPY\_DVD デコーダーの最初の bus キーを記述する BUSKEY 構造体。

<a name="remarks"></a>コメント
-------

最初のバス キーの詳細については、[DVD 著作権保護](https://msdn.microsoft.com/library/windows/hardware/ff558736)を参照してください。

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

 

 






