---
title: メモリ機能のオプションの属性
description: メモリ機能のオプションの属性
ms.assetid: 17646f6e-b234-4a17-ba24-4bc7f6f85ace
keywords:
- メモリ機能 WDK の印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec417ceb94d9b4dcdb01d0850994eb5930f184cd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531396"
---
# <a name="option-attributes-for-the-memory-feature"></a>メモリ機能のオプションの属性





次の表は、メモリの機能に関連付けられている属性を一覧表示します。 メモリ機能の詳細については、次を参照してください。[標準機能](standard-features.md)します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>属性名</th>
<th>属性パラメーター</th>
<th>コメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em><strong>MemConfigKB</strong></p></td>
<td><p>合計および使用可能なプリンター常駐メモリの (キロバイト単位) を示す数値の値のペア。 たとえば、ペアリング (1024、450) 1024 キロバイト合計、450 キロバイトのオプションの GPD によって生成された名前で、使用できることを示します&quot;1024 KB&quot;します。</p></td>
<td><p>(省略可能)。 参照してください<a href="describing-printer-memory-configurations.md" data-raw-source="[Describing Printer Memory Configurations](describing-printer-memory-configurations.md)">プリンター メモリの構成を記述する</a>します。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>MemConfigMB</strong></p></td>
<td><p>合計および使用可能なプリンター常駐メモリのメガバイト単位でことを示す数値の値のペア。 たとえば、(2, 1) のペアには、2 メガバイト、合計 1 メガバイトのオプションの GPD によって生成された名前で、使用できることを示します。 &quot;2 MB&quot;します。</p></td>
<td><p>(省略可能)。 参照してください<a href="describing-printer-memory-configurations.md" data-raw-source="[Describing Printer Memory Configurations](describing-printer-memory-configurations.md)">プリンター メモリの構成を記述する</a>します。</p></td>
</tr>
<tr class="odd">
<td><p>*<strong>MemoryConfigKB</strong></p></td>
<td><p>合計および使用可能なプリンター常駐メモリの (キロバイト単位) を示す数値の値のペア。 たとえば、ペアリング (1024、450) 1024 キロバイト単位の合計、使用可能な 450 キロバイトを示します。</p></td>
<td><p>(省略可能)。 参照してください<a href="describing-printer-memory-configurations.md" data-raw-source="[Describing Printer Memory Configurations](describing-printer-memory-configurations.md)">プリンター メモリの構成を記述する</a>します。</p></td>
</tr>
</tbody>
</table>

 

例については、次を参照してください。、[サンプル GPD ファイル](sample-gpd-files.md)します。

例については、と共に、これらの属性を使用の詳細については、次を参照してください。[プリンター メモリの構成を記述する](describing-printer-memory-configurations.md)します。

追加のオプションの属性については、次を参照してください。[すべての機能のオプション属性](option-attributes-for-all-features.md)します。

 

 




