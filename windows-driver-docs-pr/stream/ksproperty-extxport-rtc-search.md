---
title: KSK プロパティ\_EXTXPORT\_RTC\_検索
description: KSK プロパティ\_EXTXPORT\_RTC\_検索プロパティは、テープ上の相対時間カウンター (RTC) を検索します。
ms.assetid: 4a5b76fc-46f3-44f7-8548-34125df777f5
keywords:
- KSPROPERTY_EXTXPORT_RTC_SEARCH ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_EXTXPORT_RTC_SEARCH
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 436f6a5ab1d4af6901447dd96928981865e02292
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838057"
---
# <a name="ksproperty_extxport_rtc_search"></a>KSK プロパティ\_EXTXPORT\_RTC\_検索


KSK プロパティ\_EXTXPORT\_RTC\_検索プロパティは、テープ上の相対時間カウンター (RTC) を検索します。

## <span id="ddk_ksproperty_extxport_rtc_search_ks"></span><span id="DDK_KSPROPERTY_EXTXPORT_RTC_SEARCH_KS"></span>


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
<td><p>デバイス</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s)"><strong>KSPROPERTY_EXTXPORT_S</strong></a></p></td>
<td><p>DWORD</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、テープ上で検索するタイムコード (時間: 分: 秒: frame) を指定する DWORD です。

<a name="remarks"></a>注釈
-------

KSK プロパティ\_EXTXPORT\_S 構造体の**Dwtimecode コード**メンバーは、検索対象の相対時間カウンターの設定を指定します。

このメソッドは定義されていますが、サポートされていません。

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

[**KSK プロパティ\_EXTXPORT\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s)

 

 






