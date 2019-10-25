---
title: KSK プロパティ\_DVDCOPY\_TITLE\_キー
description: KSK プロパティ\_DVDCOPY\_TITLE\_キープロパティは、DVD の著作権保護の認証プロセスについて、現在のコンテンツからタイトルキー情報を取得します。
ms.assetid: 7c07bf75-cbc4-4319-a1a6-4f05d228d91a
keywords:
- KSPROPERTY_DVDCOPY_TITLE_KEY ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_DVDCOPY_TITLE_KEY
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e6784166e9a9747d35695f87e428b88b7a1a05a0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827122"
---
# <a name="ksproperty_dvdcopy_title_key"></a>KSK プロパティ\_DVDCOPY\_TITLE\_キー


KSK プロパティ\_DVDCOPY\_TITLE\_キープロパティは、DVD の著作権保護の認証プロセスについて、現在のコンテンツからタイトルキー情報を取得します。

## <span id="ddk_ksproperty_dvdcopy_title_key_ks"></span><span id="DDK_KSPROPERTY_DVDCOPY_TITLE_KEY_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_dvdcopy_titlekey" data-raw-source="[&lt;strong&gt;KS_DVDCOPY_TITLEKEY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_dvdcopy_titlekey)"><strong>KS_DVDCOPY_TITLEKEY</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、現在のタイトルキーを説明する KS\_DVDCOPY\_タイトルキーの構造体です。

<a name="remarks"></a>注釈
-------

タイトルキーの詳細については、「 [DVD Copyright Protection](https://docs.microsoft.com/windows-hardware/drivers/stream/dvd-copyright-protection)」を参照してください。

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


[**KS\_DVDCOPY\_タイトルキー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_dvdcopy_titlekey)

 

 






