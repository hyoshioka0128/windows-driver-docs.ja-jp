---
title: KSPROPERTY\_EXTXPORT\_状態\_通知
description: KSPROPERTY\_EXTXPORT\_状態\_通知プロパティを設定またはトランスポート モードと状態変更の通知を取得します。
ms.assetid: 3ebf3806-bdec-4ea2-8f2a-e75314ee020a
keywords:
- KSPROPERTY_EXTXPORT_STATE_NOTIFY ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_EXTXPORT_STATE_NOTIFY
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f12a65f5657ae7fc340bb63db169a2bb6a2c241
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354827"
---
# <a name="kspropertyextxportstatenotify"></a>KSPROPERTY\_EXTXPORT\_状態\_通知


KSPROPERTY\_EXTXPORT\_状態\_通知プロパティを設定またはトランスポート モードと状態変更の通知を取得します。

## <span id="ddk_ksproperty_extxport_state_notify_ks"></span><span id="DDK_KSPROPERTY_EXTXPORT_STATE_NOTIFY_KS"></span>


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
<td><p>〇</p></td>
<td><p>デバイス</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_extxport_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_extxport_s)"><strong>KSPROPERTY_EXTXPORT_S</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_extxport_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_extxport_s)"><strong>KSPROPERTY_EXTXPORT_S</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、KSPROPERTY\_EXTXPORT\_トランスポートの状態が変わるたびに、現在の外部のトランスポートを記述する構造。

<a name="remarks"></a>注釈
-------

KSPROPERTY\_EXTXPORT\_の構造は、トランスポートの状態が変更されたときに通知を受信します。

この呼び出しは同期操作し、トランスポートの状態が変更されるまでは返されません。 これは一部の DV camcorders はこの操作をサポートできるので、使用するため推奨されません。

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


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_EXTXPORT\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_extxport_s)

 

 






