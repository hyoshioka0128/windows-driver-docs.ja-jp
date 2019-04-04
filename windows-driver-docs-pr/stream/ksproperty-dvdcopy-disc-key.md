---
title: KSPROPERTY\_DVDCOPY\_ディスク\_キー
description: KSPROPERTY\_DVDCOPY\_ディスク\_キー プロパティ、DVD 著作権保護の認証プロセスのディスクのキー情報を取得します。
ms.assetid: 6108040e-b549-4cdc-ae1c-8f453fe5c8c1
keywords:
- KSPROPERTY_DVDCOPY_DISC_KEY ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_DVDCOPY_DISC_KEY
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff053e98431ce088782a8dd01ef9cef0bd8f3cd4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537444"
---
# <a name="kspropertydvdcopydisckey"></a>KSPROPERTY\_DVDCOPY\_ディスク\_キー


KSPROPERTY\_DVDCOPY\_ディスク\_キー プロパティ、DVD 著作権保護の認証プロセスのディスクのキー情報を取得します。

## <span id="ddk_ksproperty_dvdcopy_disc_key_ks"></span><span id="DDK_KSPROPERTY_DVDCOPY_DISC_KEY_KS"></span>


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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567637" data-raw-source="[&lt;strong&gt;KS_DVDCOPY_DISCKEY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567637)"><strong>KS_DVDCOPY_DISCKEY</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、KS\_DVDCOPY\_DISCKEY 構造体、DVD のディスクのキーについて説明します。

<a name="remarks"></a>注釈
-------

ディスク キーの詳細については、[DVD 著作権保護](https://msdn.microsoft.com/library/windows/hardware/ff558736)を参照してください。

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


[**KS\_DVDCOPY\_DISCKEY**](https://msdn.microsoft.com/library/windows/hardware/ff567637)

 

 






