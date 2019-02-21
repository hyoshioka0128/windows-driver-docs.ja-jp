---
title: アロケーター プロパティ
description: アロケーター プロパティ
ms.assetid: 851bc3d8-46f6-46d0-87a8-81de2536492a
keywords:
- アロケーター プロパティ WDK ビデオのキャプチャします。
- PROPSETID_ALLOCATOR_CONTROL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e476a82f0343f38668c4b51fe26e2badaf46c0a4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554013"
---
# <a name="allocator-properties"></a>アロケーター プロパティ


[PROPSETID\_アロケーター\_コントロール](https://msdn.microsoft.com/library/windows/hardware/ff567792)割り当てとビデオのポート画面の操作の制御に関連するプロパティがプロパティ セットに含まれています。 オーバーレイ Mixer など、ユーザー モードのフィルターを使用して、PROPSETID\_アロケーター\_コントロール。 次の表に、プロパティ、PROPSETID の一部である\_アロケーター\_コントロール プロパティのセット。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564276" data-raw-source="[&lt;strong&gt;KSPROPERTY_ALLOCATOR_CONTROL_HONOR_COUNT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564276)"><strong>KSPROPERTY_ALLOCATOR_CONTROL_HONOR_COUNT</strong></a></p></td>
<td><p>フィルターが割り当てるオーバーレイ サーフェスのビデオ ポートの数を決定する方法を制御します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564278" data-raw-source="[&lt;strong&gt;KSPROPERTY_ALLOCATOR_CONTROL_SURFACE_SIZE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564278)"><strong>KSPROPERTY_ALLOCATOR_CONTROL_SURFACE_SIZE</strong></a></p></td>
<td><p>コントロールのビデオ ポートのディメンションは、画面をオーバーレイします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564267" data-raw-source="[&lt;strong&gt;KSPROPERTY_ALLOCATOR_CONTROL_CAPTURE_CAPS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564267)"><strong>KSPROPERTY_ALLOCATOR_CONTROL_CAPTURE_CAPS</strong></a></p></td>
<td><p>ビデオ ポートのキャプチャ機能をについて説明します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564271" data-raw-source="[&lt;strong&gt;KSPROPERTY_ALLOCATOR_CONTROL_CAPTURE_INTERLEAVE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564271)"><strong>KSPROPERTY_ALLOCATOR_CONTROL_CAPTURE_INTERLEAVE</strong></a></p></td>
<td><p>返しますビデオ ポートをサポートしている場合は、キャプチャをインターリーブします。</p></td>
</tr>
</tbody>
</table>

 

 

 




