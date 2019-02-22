---
title: ユーザー インターフェイスの関数
description: ユーザー インターフェイスの関数
ms.assetid: 30ec0628-cac7-46ab-a9f2-c81ca3ad7125
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a78c397918038a31494fa7bd1137a344b77f065e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552405"
---
# <a name="user-interface-functions"></a>ユーザー インターフェイスの関数


クラスのインストーラーと共同インストーラーで、次の一般的なセットアップ関数を使用すると、現在のプロセスが、ユーザーとやり取りできるかどうかを判断します。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552207" data-raw-source="[&lt;strong&gt;SetupGetNonInteractiveMode&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552207)"><strong>SetupGetNonInteractiveMode</strong></a></p></td>
<td align="left"><p>示す SetupAPI 非対話型のフラグの値を返すかどうか、呼び出し元&#39;s プロセスがダイアログ ボックスなどのユーザー インターフェイス コンポーネントでのユーザーと対話できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552213" data-raw-source="[&lt;strong&gt;SetupSetNonInteractiveMode&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552213)"><strong>SetupSetNonInteractiveMode</strong></a></p></td>
<td align="left"><p>SetupAPI が、呼び出し元のユーザーと対話できるかどうかを決定する非対話型 SetupAPI フラグを設定&#39;s コンテキスト。</p></td>
</tr>
</tbody>
</table>

 

 

 





