---
title: KSK プロパティ\_DVDCOPY\_DEC\_KEY2
description: KSK プロパティ\_DVDCOPY\_DEC\_KEY2 プロパティは、DVD の著作権保護の認証プロセスの一環として、後でデコーダーに提供される2番目のバスキーを取得します。
ms.assetid: 48e62fec-773d-46b6-838b-5e1e457cb6a3
keywords:
- KSPROPERTY_DVDCOPY_DEC_KEY2 ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_DVDCOPY_DEC_KEY2
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc936e9eebd09379302362dcbdd407b6e8b0bc75
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843327"
---
# <a name="ksproperty_dvdcopy_dec_key2"></a>KSK プロパティ\_DVDCOPY\_DEC\_KEY2


KSK プロパティ\_DVDCOPY\_DEC\_KEY2 プロパティは、DVD の著作権保護の認証プロセスの一環として、後でデコーダーに提供される2番目のバスキーを取得します。

## <span id="ddk_ksproperty_dvdcopy_dec_key2_ks"></span><span id="DDK_KSPROPERTY_DVDCOPY_DEC_KEY2_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_dvdcopy_buskey" data-raw-source="[&lt;strong&gt;KS_DVDCOPY_BUSKEY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_dvdcopy_buskey)"><strong>KS_DVDCOPY_BUSKEY</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、DVD デコーダーの2番目のバスキーを記述する KS\_DVDCOPY\_BUSKEY 構造体です。

<a name="remarks"></a>注釈
-------

2番目のバスキーの詳細については、「 [DVD Copyright Protection](https://docs.microsoft.com/windows-hardware/drivers/stream/dvd-copyright-protection)」を参照してください。

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


[**KS\_DVDCOPY\_BUSKEY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_dvdcopy_buskey)

 

 






