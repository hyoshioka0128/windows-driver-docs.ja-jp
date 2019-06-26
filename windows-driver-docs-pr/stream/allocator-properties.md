---
title: アロケーターのプロパティ
description: アロケーターのプロパティ
ms.assetid: 851bc3d8-46f6-46d0-87a8-81de2536492a
keywords:
- アロケーター プロパティ WDK ビデオのキャプチャします。
- PROPSETID_ALLOCATOR_CONTROL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a3f5053e9951aca7b0d5d09e1b4529615d9d2ba
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386773"
---
# <a name="allocator-properties"></a>アロケーターのプロパティ


[PROPSETID\_アロケーター\_コントロール](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-allocator-control)割り当てとビデオのポート画面の操作の制御に関連するプロパティがプロパティ セットに含まれています。 オーバーレイ Mixer など、ユーザー モードのフィルターを使用して、PROPSETID\_アロケーター\_コントロール。 次の表に、プロパティ、PROPSETID の一部である\_アロケーター\_コントロール プロパティのセット。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>PROPSETID_ALLOCATOR_CONTROL KS properties</th>
<th>プロパティの説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-allocator-control-honor-count" data-raw-source="[&lt;strong&gt;KSPROPERTY_ALLOCATOR_CONTROL_HONOR_COUNT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-allocator-control-honor-count)"><strong>KSPROPERTY_ALLOCATOR_CONTROL_HONOR_COUNT</strong></a></p></td>
<td><p>フィルターが割り当てるオーバーレイ サーフェスのビデオ ポートの数を決定する方法を制御します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-allocator-control-surface-size" data-raw-source="[&lt;strong&gt;KSPROPERTY_ALLOCATOR_CONTROL_SURFACE_SIZE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-allocator-control-surface-size)"><strong>KSPROPERTY_ALLOCATOR_CONTROL_SURFACE_SIZE</strong></a></p></td>
<td><p>コントロールのビデオ ポートのディメンションは、画面をオーバーレイします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-allocator-control-capture-caps" data-raw-source="[&lt;strong&gt;KSPROPERTY_ALLOCATOR_CONTROL_CAPTURE_CAPS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-allocator-control-capture-caps)"><strong>KSPROPERTY_ALLOCATOR_CONTROL_CAPTURE_CAPS</strong></a></p></td>
<td><p>ビデオ ポートのキャプチャ機能をについて説明します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-allocator-control-capture-interleave" data-raw-source="[&lt;strong&gt;KSPROPERTY_ALLOCATOR_CONTROL_CAPTURE_INTERLEAVE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-allocator-control-capture-interleave)"><strong>KSPROPERTY_ALLOCATOR_CONTROL_CAPTURE_INTERLEAVE</strong></a></p></td>
<td><p>返しますビデオ ポートをサポートしている場合は、キャプチャをインターリーブします。</p></td>
</tr>
</tbody>
</table>

 

 

 




