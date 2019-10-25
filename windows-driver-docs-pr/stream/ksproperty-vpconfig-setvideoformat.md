---
title: KSK プロパティの\_VPCONFIG\_SETVIDEOFORMAT
description: KSPROPERTY\_VPCONFIG\_SETVIDEOFORMAT プロパティは、ビデオ形式を設定します。 この形式は、以前の KSK プロパティ\_の VPCONFIG\_GETVIDEOFORMAT Get 要求が返されたものと一致している必要があります。
ms.assetid: f701ad32-ba85-4766-ac6b-11744af8fc0d
keywords:
- KSPROPERTY_VPCONFIG_SETVIDEOFORMAT ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_VPCONFIG_SETVIDEOFORMAT
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6da877bb342aa25a3205af65ff645173481a863d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823622"
---
# <a name="ksproperty_vpconfig_setvideoformat"></a>KSK プロパティの\_VPCONFIG\_SETVIDEOFORMAT


KSPROPERTY\_VPCONFIG\_SETVIDEOFORMAT プロパティは、ビデオ形式を設定します。 この形式は、以前の KSK プロパティ\_の VPCONFIG\_GETVIDEOFORMAT **Get**要求が返されたものと一致している必要があります。

## <span id="ddk_ksproperty_vpconfig_setvideoformat_ks"></span><span id="DDK_KSPROPERTY_VPCONFIG_SETVIDEOFORMAT_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddpixelformat" data-raw-source="[&lt;strong&gt;DDPIXELFORMAT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddpixelformat)"><strong>DDピクセル形式</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、使用するビデオ形式を指定する、DDピクセル形式の構造体です。

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


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**DDピクセル形式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddpixelformat)

 

 






