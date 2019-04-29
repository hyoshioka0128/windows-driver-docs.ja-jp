---
title: データ クラス インターフェイス
description: データ クラス インターフェイス
ms.assetid: d7bf9ec3-8bf3-45a9-84a2-c507953d1ad4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b16b280d233c3e4142db334d16e853ba3e3361e1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387389"
---
# <a name="data-class-interface"></a>データ クラス インターフェイス





データ クラス インターフェイスは、標準の 2 つのエンドポイント記述子続けて USB インターフェイス記述子によって記述されます。 データ クラス インターフェイス内の 2 つのエンドポイント記述子が USB 一括型の標準エンドポイントを定義します。 1 つの一括 IN と 1 つの一括アウト。 次の表では、データ クラス インターフェイスの記述子の著名なフィールドを定義します。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">オフセット (バイト)</th>
<th align="left">フィールド</th>
<th align="left">サイズ (バイト)</th>
<th align="left">値</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>5</p></td>
<td align="left"><p>bInterfaceClass</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0 ah</p></td>
<td align="left"><p>データ インターフェイス クラスのコードです。</p></td>
</tr>
<tr class="even">
<td align="left"><p>6</p></td>
<td align="left"><p>bInterfaceSubClass</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>00 h</p></td>
<td align="left"><p>データ クラスのサブクラス コードです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>7</p></td>
<td align="left"><p>bInterfaceProtocol</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>00 h</p></td>
<td align="left"><p>データ クラス プロトコルのコードです。</p></td>
</tr>
</tbody>
</table>

 

 

 





