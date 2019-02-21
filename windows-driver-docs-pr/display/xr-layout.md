---
title: XR レイアウト
description: XR レイアウト
ms.assetid: a5c5d627-8d1a-4091-a7b2-893165e7fe45
keywords:
- Direct3D バージョン 10.1 WDK Windows 7 の表示、XR レイアウト
- 拡張形式、Windows 7 の WDK 表示 XR レイアウト
- XR レイアウト WDK Windows 7 の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd57d97309dc269986cd3571215a3f1d1a920d06
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535738"
---
# <a name="xr-layout"></a>XR レイアウト


このセクションでは、Windows 7 およびそれ以降のオペレーティング システムにのみ適用されます。

ダンプは、固定小数点 1.9 形式です。 値は、その結果、ダイナミック レンジは約-0.5 バイアス\[-0.5,1.5\]します。 固定小数点表記は、小数点以下桁数が小数点 10 進数の 1 つの場所を右にシフトする 2 倍を意味します。

各 XR 要素は、ホスト CPU エンディアンに関係なく、次の表に示すようにレイアウトが 1 つの 32-ビット DWORD を占有します。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Bits 31:30</th>
<th align="left">Bits 29:20</th>
<th align="left">ビットを 19時 10分</th>
<th align="left">ビット 9:0</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>アルファ チャネル</p></td>
<td align="left"><p>青チャネル</p></td>
<td align="left"><p>緑チャネル</p></td>
<td align="left"><p>赤チャネル</p></td>
</tr>
</tbody>
</table>

 

次の表に示すように、赤、緑、青チャネルの各レイアウトは。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ビット 9</th>
<th align="left">ビット 8:0</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1 ビットの整数部分</p></td>
<td align="left"><p>小数部の 9 ビット</p></td>
</tr>
</tbody>
</table>

 

 

 





