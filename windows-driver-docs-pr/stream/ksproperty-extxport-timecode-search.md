---
title: KSK プロパティ\_EXTXPORT\_タイムコード\_検索
description: KSK プロパティ\_EXTXPORT\_タイムコード\_検索プロパティは、特定のタイムコードを検索します。
ms.assetid: 34252fce-426b-4f75-b57f-fa86654ffc5f
keywords:
- KSPROPERTY_EXTXPORT_TIMECODE_SEARCH ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_EXTXPORT_TIMECODE_SEARCH
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c660bf134de6f8140dbdb96f19eaffa2e7293a1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827008"
---
# <a name="ksproperty_extxport_timecode_search"></a>KSK プロパティ\_EXTXPORT\_タイムコード\_検索


KSK プロパティ\_EXTXPORT\_タイムコード\_検索プロパティは、特定のタイムコードを検索します。

## <span id="ddk_ksproperty_extxport_timecode_search_ks"></span><span id="DDK_KSPROPERTY_EXTXPORT_TIMECODE_SEARCH_KS"></span>


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
<td><p>埋め込まれた<strong>タイムコード</strong>構造</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、フレーム、秒、分、時間など、検索する特定のタイムコードを記述する KSK プロパティ\_EXTXPORT\_S 構造体の埋め込みの**タイムコード**構造体メンバーです。

<a name="remarks"></a>注釈
-------

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

 

 






