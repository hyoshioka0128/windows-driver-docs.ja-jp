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
ms.openlocfilehash: eead2c7b46b8aa683b118c6d18782a4fc02e5380
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373063"
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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ks_dvdcopy_disckey" data-raw-source="[&lt;strong&gt;KS_DVDCOPY_DISCKEY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ks_dvdcopy_disckey)"><strong>KS_DVDCOPY_DISCKEY</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、KS\_DVDCOPY\_DISCKEY 構造体、DVD のディスクのキーについて説明します。

<a name="remarks"></a>注釈
-------

ディスク キーの詳細については、次を参照してください。 [DVD 著作権保護](https://docs.microsoft.com/windows-hardware/drivers/stream/dvd-copyright-protection)します。

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


[**KS\_DVDCOPY\_DISCKEY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ks_dvdcopy_disckey)

 

 






