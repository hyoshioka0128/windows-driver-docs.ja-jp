---
title: KSK プロパティ\_MEDIASEEKING\_機能
description: KSK プロパティ\_MEDIASEEKING\_CAPABILITIES プロパティは、フィルターのメディアシーク機能を取得します。
ms.assetid: f0ee8fed-cdb5-44f9-96c3-d6edf235ea35
keywords:
- KSPROPERTY_MEDIASEEKING_CAPABILITIES ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_MEDIASEEKING_CAPABILITIES
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b483e365e8fcb36f1994daf5bb871882475939d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838047"
---
# <a name="ksproperty_mediaseeking_capabilities"></a>KSK プロパティ\_MEDIASEEKING\_機能


KSK プロパティ\_MEDIASEEKING\_CAPABILITIES プロパティは、フィルターのメディアシーク機能を取得します。

## <span id="ddk_ksproperty_mediaseeking_capabilities_ks"></span><span id="DDK_KSPROPERTY_MEDIASEEKING_CAPABILITIES_KS"></span>


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
<td><p>フィルター</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p>KS_SEEKING_CAPABILITIES</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

このプロパティによって取得されるフィルターの機能には、絶対位置にシークする機能、メディア内で前方または後方をシークする機能、再生モードまたは停止モードでの現在の位置を取得する機能、期間を取得する機能、または逆方向に再生する機能が含まれます。 これらはフィルター全体の機能であることに注意してください。このプロパティは、このような機能が pin ではなくフィルターのみで照会される、DirectShow シーク機能にマップするように設計されています。

このプロパティがサポートされていない場合は、フィルターが位置情報を必要とせず、フィルターをパススルーとして扱うことができることを前提としています。

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
<td>Ks (Ks を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[KSPROPSETID\_MediaSeeking](kspropsetid-mediaseeking.md)

 

 






