---
title: KSPROPERTY\_EXTDEVICE\_POWER\_状態
description: KSPROPERTY\_EXTDEVICE\_POWER\_状態プロパティを設定または外部のデバイスの電源状態を取得します。
ms.assetid: bfca1f3d-b563-4ddd-b823-85487b4a4093
keywords:
- KSPROPERTY_EXTDEVICE_POWER_STATE ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_EXTDEVICE_POWER_STATE
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: de7c838efefeef435bdf931785c2e26394684577
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354861"
---
# <a name="kspropertyextdevicepowerstate"></a>KSPROPERTY\_EXTDEVICE\_POWER\_状態


KSPROPERTY\_EXTDEVICE\_POWER\_状態プロパティを設定または外部のデバイスの電源状態を取得します。

## <span id="ddk_ksproperty_extdevice_power_state_ks"></span><span id="DDK_KSPROPERTY_EXTDEVICE_POWER_STATE_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_extdevice_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTDEVICE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_extdevice_s)"><strong>KSPROPERTY_EXTDEVICE_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、外部のデバイスの電源の状態を指定する ULONG です。

<a name="remarks"></a>注釈
-------

**PowerState** 、KSPROPERTY のメンバー\_EXTDEVICE\_構造が外部のデバイスの電源設定を指定します。 **PowerState**に等しいまたはスタンバイにメンバーを設定することがあります。 たとえば、バッテリ駆動外部などのデバイス、DV カメラを電源オフ可能性があります。 AC 電源 DVHS デバイスは、スタンバイに配置することがあります。 デバイスがスタンバイ状態にある場合、電源をオンに後でする可能性があります。

<a name="requirements"></a>必要条件
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

[**KSPROPERTY\_EXTDEVICE\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_extdevice_s)

 

 






