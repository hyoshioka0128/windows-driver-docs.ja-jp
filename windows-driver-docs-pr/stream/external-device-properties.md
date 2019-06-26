---
title: 外部デバイスのプロパティ
description: 外部デバイスのプロパティ
ms.assetid: 633b24c7-a1da-4748-aaa2-864a01a3fd98
keywords:
- 外部のデバイス プロパティ WDK ビデオのキャプチャします。
- PROPSETID_EXT_DEVICE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17cffc125259090ff9f9d9848c082a04b08c09ad
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384087"
---
# <a name="external-device-properties"></a>外部デバイスのプロパティ


[PROPSETID\_EXT\_デバイス](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-ext-device)コントロールかビデオ_カメラまたはデジタルのテープ デッキなどの外部のデバイスの操作に関連するプロパティがプロパティ セットに含まれています。 次の表に、プロパティ、PROPSETID の一部である\_EXT\_デバイス プロパティのセット。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>PROPSETID_EXT_DEVICE KS プロパティ</th>
<th>プロパティの説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extdevice-id" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTDEVICE_ID&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extdevice-id)"><strong>KSPROPERTY_EXTDEVICE_ID</strong></a></p></td>
<td><p>外部のデバイスの汎用システム全体の id。 を返します</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extdevice-version" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTDEVICE_VERSION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extdevice-version)"><strong>KSPROPERTY_EXTDEVICE_VERSION</strong></a></p></td>
<td><p>外部デバイスのバージョンを返します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extdevice-power-state" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTDEVICE_POWER_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extdevice-power-state)"><strong>KSPROPERTY_EXTDEVICE_POWER_STATE</strong></a></p></td>
<td><p>、スタンバイ状態で、またはオフなどの外部デバイスの電源状態を制御します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extdevice-port" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTDEVICE_PORT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extdevice-port)"><strong>KSPROPERTY_EXTDEVICE_PORT</strong></a></p></td>
<td><p>外部デバイスの接続ポートの種類、1394 などまたは USB を返します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extdevice-capabilities" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTDEVICE_CAPABILITIES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-extdevice-capabilities)"><strong>KSPROPERTY_EXTDEVICE_CAPABILITIES</strong></a></p></td>
<td><p>ビデオの機能を所有するデバイスが記録できるかどうかなど、外部のデバイスの機能や、デバイスがファイルを使用して返します。</p></td>
</tr>
</tbody>
</table>

 

 

 




