---
title: ユーザー インターフェイス関数
description: ユーザー インターフェイス関数
ms.assetid: 30ec0628-cac7-46ab-a9f2-c81ca3ad7125
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc2dcfa9e12430fb9abe737877eba295e440b9ac
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350037"
---
# <a name="user-interface-functions"></a>ユーザー インターフェイス関数


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
<td align="left"><p>呼び出し元のプロセスがダイアログ ボックスなどのユーザー インターフェイス コンポーネントでのユーザーと対話できるかどうかを示す SetupAPI 非対話型フラグの値を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552213" data-raw-source="[&lt;strong&gt;SetupSetNonInteractiveMode&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552213)"><strong>SetupSetNonInteractiveMode</strong></a></p></td>
<td align="left"><p>SetupAPI が呼び出し元のコンテキスト内のユーザーと対話できるかどうかを決定する非対話型 SetupAPI フラグを設定します。</p></td>
</tr>
</tbody>
</table>

 

 

 





