---
title: KSPROPERTY\_DVDCOPY\_DEC\_KEY2
description: KSPROPERTY\_DVDCOPY\_DEC\_KEY2 プロパティは、DVD 著作権保護の認証プロセスの一環として、デコーダーに後で提供される 2 つ目のバス キーを取得します。
ms.assetid: 48e62fec-773d-46b6-838b-5e1e457cb6a3
keywords:
- KSPROPERTY_DVDCOPY_DEC_KEY2 ストリーミング メディア デバイス
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
ms.openlocfilehash: 42262ae408d995d3bc25626f7c8795bc899a5474
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373060"
---
# <a name="kspropertydvdcopydeckey2"></a>KSPROPERTY\_DVDCOPY\_DEC\_KEY2


KSPROPERTY\_DVDCOPY\_DEC\_KEY2 プロパティは、DVD 著作権保護の認証プロセスの一環として、デコーダーに後で提供される 2 つ目のバス キーを取得します。

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
<td><p>いいえ</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ks_dvdcopy_buskey" data-raw-source="[&lt;strong&gt;KS_DVDCOPY_BUSKEY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ks_dvdcopy_buskey)"><strong>KS_DVDCOPY_BUSKEY</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、KS\_DVDCOPY\_DVD デコーダーの 2 つ目のバス キーを記述する BUSKEY 構造体。

<a name="remarks"></a>注釈
-------

バスの 2 番目のキーの詳細については、次を参照してください。 [DVD 著作権保護](https://docs.microsoft.com/windows-hardware/drivers/stream/dvd-copyright-protection)します。

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


[**KS\_DVDCOPY\_BUSKEY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ks_dvdcopy_buskey)

 

 






