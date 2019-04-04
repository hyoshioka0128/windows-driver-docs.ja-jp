---
title: DVD に関連したクロック関数
description: DVD に関連したクロック関数
ms.assetid: 495f25dc-cd79-4f7f-acbc-b8b271269fb3
keywords:
- DVD デコーダー ミニドライバー WDK、マスターのクロック
- デコーダー ミニドライバー WDK DVD、マスターのクロック
- マスターのクロックの WDK DVD デコーダー
- WDK DVD デコーダーをクロックします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f11e19af62d483e943fae8ef1f6d41a91e09b159
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556664"
---
# <a name="dvd-related-clock-functions"></a>DVD に関連したクロック関数





クロックのすべてのハンドルは、適切な個別のストリームに格納する必要があります。 グローバルまたは静的変数でない保存します。 詳細については、[KS クロック](ks-clocks.md)を参照してください。

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

 

 

 




