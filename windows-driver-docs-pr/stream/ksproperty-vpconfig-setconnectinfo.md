---
title: KSPROPERTY\_VPCONFIG\_SETCONNECTINFO
description: KSPROPERTY\_VPCONFIG\_SETCONNECTINFO プロパティは、ユーザー定義の接続情報を使用してビデオポート構成を設定します。 これは、KSK プロパティ\_VPCONFIG\_GETCONNECTINFO プロパティによって返される、DDVIDEOPORTCONNECT 構造体の配列へのポインターです。
ms.assetid: 120f6889-cd67-4c05-b4b8-adab3efd7f2c
keywords:
- KSPROPERTY_VPCONFIG_SETCONNECTINFO ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_VPCONFIG_SETCONNECTINFO
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5e98ec6b7ff3815b740910ef17b66ab6d444683
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823663"
---
# <a name="ksproperty_vpconfig_setconnectinfo"></a>KSPROPERTY\_VPCONFIG\_SETCONNECTINFO


KSPROPERTY\_VPCONFIG\_SETCONNECTINFO プロパティは、ユーザー定義の接続情報を使用してビデオポート構成を設定します。 これは、KSK プロパティ\_VPCONFIG\_GETCONNECTINFO プロパティによって返される、 [**Ddvideoportconnect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddvideoportconnect)構造体の配列へのポインターです。

## <span id="ddk_ksproperty_vpconfig_setconnectinfo_ks"></span><span id="DDK_KSPROPERTY_VPCONFIG_SETCONNECTINFO_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddvideoportconnect" data-raw-source="[&lt;strong&gt;DDVIDEOPORTCONNECT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddvideoportconnect)"><strong>DDVIDEOPORTCONNECT</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、ビデオポート接続の構成を記述する DDVIDEOPORTCONNECT 構造体です。

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


[**DDVIDEOPORTCONNECT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddvideoportconnect)

[**KSK プロパティ\_VPCONFIG\_GETCONNECTINFO**](ksproperty-vpconfig-getconnectinfo.md)

 

 






