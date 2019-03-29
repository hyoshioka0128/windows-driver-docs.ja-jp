---
title: GDI セマフォ サービス
description: GDI セマフォ サービス
ms.assetid: b91211a7-19c3-4974-9222-f8eb64c29cc8
keywords:
- GDI WDK Windows 2000 の表示、セマフォ サービス
- WDK Windows 2000 を表示するグラフィック ドライバー サービスをセマフォします。
- サービスをセマフォ WDK GDI を描画するには、
- サービス WDK GDI をセマフォします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22bfacdab96dcf621e2bce474be77a41a4deb4b8
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349099"
---
# <a name="gdi-semaphore-services"></a>GDI セマフォ サービス


## <span id="ddk_gdi_semaphore_services_gg"></span><span id="DDK_GDI_SEMAPHORE_SERVICES_GG"></span>


GDI は、セマフォや安全なセマフォに関連するサービスの選択範囲を提供します。 ドライバーは、作成や、セマフォを削除し、取得またはセマフォを解放するこれらのサービスを使用できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">関数</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564174" data-raw-source="[&lt;strong&gt;EngAcquireSemaphore&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564174)"><strong>EngAcquireSemaphore</strong></a></p></td>
<td align="left"><p>呼び出し元のスレッドにより排他アクセスのセマフォに関連付けられたリソースを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564760" data-raw-source="[&lt;strong&gt;EngCreateSemaphore&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564760)"><strong>EngCreateSemaphore</strong></a></p></td>
<td align="left"><p>セマフォ オブジェクトを作成します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564814" data-raw-source="[&lt;strong&gt;EngDeleteSafeSemaphore&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564814)"><strong>EngDeleteSafeSemaphore</strong></a></p></td>
<td align="left"><p>指定した安全なセマフォへの参照を削除します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564819" data-raw-source="[&lt;strong&gt;EngDeleteSemaphore&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564819)"><strong>EngDeleteSemaphore</strong></a></p></td>
<td align="left"><p>システムのリソースの一覧から、セマフォ オブジェクトを削除します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564959" data-raw-source="[&lt;strong&gt;EngInitializeSafeSemaphore&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564959)"><strong>EngInitializeSafeSemaphore</strong></a></p></td>
<td align="left"><p>指定した安全なセマフォを初期化します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564960" data-raw-source="[&lt;strong&gt;EngIsSemaphoreOwned&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564960)"><strong>EngIsSemaphoreOwned</strong></a></p></td>
<td align="left"><p>任意のスレッドが、指定したセマフォを保持しているかどうかを判断します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564961" data-raw-source="[&lt;strong&gt;EngIsSemaphoreOwnedByCurrentThread&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564961)"><strong>EngIsSemaphoreOwnedByCurrentThread</strong></a></p></td>
<td align="left"><p>現在実行中のスレッドが、指定したセマフォを保持しているかどうかを判断します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565004" data-raw-source="[&lt;strong&gt;EngReleaseSemaphore&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565004)"><strong>EngReleaseSemaphore</strong></a></p></td>
<td align="left"><p>指定したセマフォを解放します。</p></td>
</tr>
</tbody>
</table>

 

 

 





