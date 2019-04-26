---
title: ドライバーのランクの範囲
description: ドライバーのランクの範囲
ms.assetid: ea822171-c1f3-49b4-ae63-3300728666f0
keywords:
- ドライバーのランクの範囲は WDK デバイスのインストール
- ランクの範囲は WDK デバイスのインストール
- WDK のデバイスのインストールを順位付けの範囲
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ae40fb83399ff1a8b68f2347d54b6d392dc1d77
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356008"
---
# <a name="driver-rank-ranges"></a>ドライバーのランクの範囲


ドライバーのランクは 0 x として書式設定*SSGGTHHH*ここで、0 x の値*SS*000000、[署名スコア](signature-score--windows-vista-and-later-.md)、0x00 の値*GG*0000 です[機能のスコア](feature-score--windows-vista-and-later-.md)、し、値 0x0000*THHH*は、[識別子スコア](identifier-score--windows-vista-and-later-.md)。

次の表に、範囲を一覧表示すべて有効なドライバー順位付け、0 x*SS*000000 は 0x00 で、有効な署名スコアを表す*GG*0000 表す有効な特徴のスコア、およびの識別子の範囲がスコア付け識別子の一致の種類ごとに表示されます。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ドライバーのランク</th>
<th align="left">識別子のスコア</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0xSS<em>GG</em>0000 0xSS<em>GG</em>0 fff</p></td>
<td align="left"><p>0x0000 0x0FFF</p></td>
<td align="left"><p>デバイスのハードウェア ID には、INF 内のハードウェア ID が一致する<em>モデル</em>セクション エントリ。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xSS<em>GG</em>1000 0xSS<em>GG</em>1 fff</p></td>
<td align="left"><p>0x1000 0x1FFF</p></td>
<td align="left"><p>デバイスのハードウェア ID には、INF で互換性のある ID が一致する<em>モデル</em>セクション エントリ。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xSS<em>GG</em>2000 0xSS<em>GG</em>2 fff</p></td>
<td align="left"><p>0x2000 から 0x2FFF</p></td>
<td align="left"><p>デバイスの互換性のある ID には、INF 内のハードウェア ID が一致する<em>モデル</em>セクション エントリ。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xSS<em>GG</em>3000 0xSS<em>GG</em>3FFF</p></td>
<td align="left"><p>0x3000 から 0x3FFF</p></td>
<td align="left"><p>デバイスの互換性のある ID には、INF で互換性のある ID が一致する<em>モデル</em>セクション エントリ。</p></td>
</tr>
</tbody>
</table>

 

 

 





