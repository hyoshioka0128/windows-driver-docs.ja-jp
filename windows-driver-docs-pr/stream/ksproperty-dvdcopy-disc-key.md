---
title: KSK プロパティ\_DVDCOPY\_ディスク\_キー
description: KSK プロパティ\_DVDCOPY\_ディスク\_キープロパティは、DVD の著作権保護認証プロセスのディスクキー情報を取得します。
ms.assetid: 6108040e-b549-4cdc-ae1c-8f453fe5c8c1
keywords:
- KSPROPERTY_DVDCOPY_DISC_KEY ストリーミングメディアデバイス
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
ms.openlocfilehash: 254ef660d9af9e53b4b3523c3b776526057ee7e9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844311"
---
# <a name="ksproperty_dvdcopy_disc_key"></a>KSK プロパティ\_DVDCOPY\_ディスク\_キー


KSK プロパティ\_DVDCOPY\_ディスク\_キープロパティは、DVD の著作権保護認証プロセスのディスクキー情報を取得します。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_dvdcopy_disckey" data-raw-source="[&lt;strong&gt;KS_DVDCOPY_DISCKEY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_dvdcopy_disckey)"><strong>KS_DVDCOPY_DISCKEY</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、DVD のディスクキーを記述する KS\_DVDCOPY\_DISCKEY 構造体です。

<a name="remarks"></a>注釈
-------

ディスクキーの詳細については、「 [DVD Copyright Protection](https://docs.microsoft.com/windows-hardware/drivers/stream/dvd-copyright-protection)」を参照してください。

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


[**KS\_DVDCOPY\_DISCKEY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_dvdcopy_disckey)

 

 






