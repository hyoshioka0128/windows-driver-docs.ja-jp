---
title: KSK プロパティ\_ATN\_READER
description: KSK プロパティ\_ATN\_READER プロパティは、現在のテープの位置の絶対トラック番号 (ATN) を取得します。
ms.assetid: ac127aa0-5a47-41b2-9a2d-96090231d43e
keywords:
- KSPROPERTY_ATN_READER ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_ATN_READER
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e42cc5d1e19a806a57e7fb4b3af7b42fdb24a82
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831999"
---
# <a name="ksproperty_atn_reader"></a>KSK プロパティ\_ATN\_READER


KSK プロパティ\_ATN\_READER プロパティは、現在のテープの位置の絶対トラック番号 (ATN) を取得します。

## <span id="ddk_ksproperty_atn_reader_ks"></span><span id="DDK_KSPROPERTY_ATN_READER_KS"></span>


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
<td><p>デバイス</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_timecode_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_TIMECODE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_timecode_s)"><strong>KSPROPERTY_TIMECODE_S</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagtimecode_sample" data-raw-source="[&lt;strong&gt;TIMECODE_SAMPLE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagtimecode_sample)"><strong>TIMECODE_SAMPLE</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、現在のテープの位置の絶対トラック番号を指定するタイムコード\_のサンプル構造です。

<a name="remarks"></a>注釈
-------

KSK プロパティの**TimecodeSamp**メンバー\_タイムコード\_S 構造体は、現在のテープの位置の絶対トラック番号を表します。

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

[**KSK プロパティ\_タイムコード\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_timecode_s)

[**タイムコード\_のサンプル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagtimecode_sample)

 

 






