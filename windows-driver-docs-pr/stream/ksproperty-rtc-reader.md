---
title: KSK プロパティ\_RTC\_READER
description: KSK プロパティ\_RTC\_READER プロパティは、現在のテープの位置の相対時間カウンター (RTC) を取得します。
ms.assetid: 728a4504-de60-47c7-a381-3513f2d4745b
keywords:
- KSPROPERTY_RTC_READER ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_RTC_READER
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed71a1b0ab3d66e335374bd8b7441bc8316d6418
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838831"
---
# <a name="ksproperty_rtc_reader"></a>KSK プロパティ\_RTC\_READER


KSK プロパティ\_RTC\_READER プロパティは、現在のテープの位置の相対時間カウンター (RTC) を取得します。

## <span id="ddk_ksproperty_rtc_reader_ks"></span><span id="DDK_KSPROPERTY_RTC_READER_KS"></span>


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

 

プロパティ値 (操作データ) は、現在のテープの位置の相対時間カウンターを指定する、タイムコード\_のサンプル構造です。

<a name="remarks"></a>注釈
-------

KSK プロパティの**TimecodeSamp**メンバー\_タイムコード\_S 構造体は、現在のテープの位置の相対時間カウンターを表します。

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

 

 






