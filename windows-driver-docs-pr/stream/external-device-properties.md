---
title: 外部デバイスのプロパティ
description: 外部デバイスのプロパティ
ms.assetid: 633b24c7-a1da-4748-aaa2-864a01a3fd98
keywords:
- 外部のデバイス プロパティ WDK ビデオのキャプチャします。
- PROPSETID_EXT_DEVICE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6dc036620e340ed2fba5e4e234985cd925887c15
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531594"
---
# <a name="external-device-properties"></a>外部デバイスのプロパティ


[PROPSETID\_EXT\_デバイス](https://msdn.microsoft.com/library/windows/hardware/ff567795)コントロールかビデオ_カメラまたはデジタルのテープ デッキなどの外部のデバイスの操作に関連するプロパティがプロパティ セットに含まれています。 次の表に、プロパティ、PROPSETID の一部である\_EXT\_デバイス プロパティのセット。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565153" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTDEVICE_ID&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565153)"><strong>KSPROPERTY_EXTDEVICE_ID</strong></a></p></td>
<td><p>外部デバイスを返します&#39;s 一般化システム全体の id。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565157" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTDEVICE_VERSION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565157)"><strong>KSPROPERTY_EXTDEVICE_VERSION</strong></a></p></td>
<td><p>外部デバイスのバージョンを返します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565155" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTDEVICE_POWER_STATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565155)"><strong>KSPROPERTY_EXTDEVICE_POWER_STATE</strong></a></p></td>
<td><p>、スタンバイ状態で、またはオフなどの外部デバイスの電源状態を制御します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565154" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTDEVICE_PORT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565154)"><strong>KSPROPERTY_EXTDEVICE_PORT</strong></a></p></td>
<td><p>外部デバイスを返します&#39;1394 など、接続ポートの s の型、または USB です。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565152" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTDEVICE_CAPABILITIES&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565152)"><strong>KSPROPERTY_EXTDEVICE_CAPABILITIES</strong></a></p></td>
<td><p>ビデオの機能を所有するデバイスが記録できるかどうかなど、外部のデバイスの機能や、デバイスがファイルを使用して返します。</p></td>
</tr>
</tbody>
</table>

 

 

 




