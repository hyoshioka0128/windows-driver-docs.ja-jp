---
title: DVD 関連のクロック関数
description: DVD 関連のクロック関数
ms.assetid: 495f25dc-cd79-4f7f-acbc-b8b271269fb3
keywords:
- DVD デコーダー ミニドライバー WDK、マスターのクロック
- デコーダー ミニドライバー WDK DVD、マスターのクロック
- マスターのクロックの WDK DVD デコーダー
- WDK DVD デコーダーをクロックします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f11e19af62d483e943fae8ef1f6d41a91e09b159
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363826"
---
# <a name="dvd-related-clock-functions"></a>DVD 関連のクロック関数





クロックのすべてのハンドルは、適切な個別のストリームに格納する必要があります。 グローバルまたは静的変数でない保存します。 詳細については、次を参照してください。 [KS クロック](ks-clocks.md)します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>関数</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568190" data-raw-source="[&lt;strong&gt;SRB_OPEN_MASTER_CLOCK&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568190)"><strong>SRB_OPEN_MASTER_CLOCK</strong></a></p></td>
<td><p>DVD デコーダー ミニドライバーに、指定したストリームがマスター制が開かれると、そのクロックにアクセスするため、DVD デコーダー ミニドライバー マスター クロック ルーチンの呼び出しはすべてで使用されるマスター クロック ハンドルを提供することを示します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568163" data-raw-source="[&lt;strong&gt;SRB_CLOSE_MASTER_CLOCK&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568163)"><strong>SRB_CLOSE_MASTER_CLOCK</strong></a></p></td>
<td><p>指定されたマスター クロック ハンドルがアクティブでなくなったことを示します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568179" data-raw-source="[&lt;strong&gt;SRB_INDICATE_MASTER_CLOCK&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568179)"><strong>SRB_INDICATE_MASTER_CLOCK</strong></a></p></td>
<td><p>時間の通話ルーティング オーケストレーションは、ときに使用されるハンドルのすべてのストリームを提供します。</p></td>
</tr>
</tbody>
</table>

 

 

 




