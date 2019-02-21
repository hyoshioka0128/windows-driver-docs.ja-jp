---
title: Unidrv キーワード
description: Unidrv キーワード
ms.assetid: b76fcf53-cd75-4e85-a7a2-00a69cc82a97
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 34c61e9b7354c9f81290f7c639dd640ec0ab7a61
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539687"
---
# <a name="unidrv-keywords"></a>Unidrv キーワード


Unidrv プラグインは、文字列を使用して、メソッドの呼び出しのヘルパー インターフェイス上の構成ファイルの GPD ビュー (GDL ビューではなく) に表示される必要があります。 さらに、Unidrv で提供される機能は、パーセント記号 (%) で前に付きます。 次の表では、サポートされているシミュレートされた機能を示します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>機能名</th>
<th>オプション</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>% MetafileSpooling</td>
<td><p></p>
&quot;True&quot; &quot;False&quot;</td>
<td><p>EMF スプールを有効にします。</p>
<p>ドキュメントの付箋。</p></td>
</tr>
<tr class="even">
<td><p><strong>%PageOrder</strong></p></td>
<td><p>&quot;FrontToBack&quot;</p>
<p>&quot;BackToFront&quot;</p></td>
<td><p>ページの印刷順序を指定します。</p>
<p>この機能は、プリント プロセッサは EMF スプールを実行できない場合にのみ使用できます。</p>
<p>ドキュメントの付箋。</p></td>
</tr>
<tr class="odd">
<td><p><strong>%PagePerSheet</strong></p></td>
<td><p></p>
&quot;1&quot;、 &quot;2&quot;、 &quot;4&quot;、6&quot;、 &quot;9&quot;、 &quot;16&quot;、&quot;小冊子&quot;</td>
<td><p>物理ページに印刷されている論理ページの数を指定します。 &quot;小冊子&quot;オプションは、双方向の機能が定義されている場合にのみ使用できます。</p>
<p>この機能は、プリント プロセッサは EMF スプールを実行できない場合にのみ使用できます。</p>
<p>ドキュメントの付箋。</p></td>
</tr>
<tr class="even">
<td><p><strong>% TextAsGraphics</strong></p></td>
<td><p></p>
&quot;True&quot; &quot;False&quot;</td>
<td><p>グラフィックスとテキストを印刷します。</p>
<p>ドキュメントの付箋。</p></td>
</tr>
</tbody>
</table>

 

GPD の構文が一部は、作成機能とオプションの解析時に展開されます。 このカテゴリに分類される最も一般的な構文は、 \* **MemConfigKB**キーワード。 他のユーザーが含まれて、 \* **MemConfigMB**、 \* **MemoryConfigKB**、および\***インストール可能**キーワード。

 

 




