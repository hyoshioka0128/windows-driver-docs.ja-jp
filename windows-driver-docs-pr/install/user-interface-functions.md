---
title: ユーザー インターフェイス関数
description: ユーザー インターフェイス関数
ms.assetid: 30ec0628-cac7-46ab-a9f2-c81ca3ad7125
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9934d982dbeab42b29e0b734c5b6e0c937cf869
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380451"
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
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupgetnoninteractivemode" data-raw-source="[&lt;strong&gt;SetupGetNonInteractiveMode&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupgetnoninteractivemode)"><strong>SetupGetNonInteractiveMode</strong></a></p></td>
<td align="left"><p>呼び出し元のプロセスがダイアログ ボックスなどのユーザー インターフェイス コンポーネントでのユーザーと対話できるかどうかを示す SetupAPI 非対話型フラグの値を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupsetnoninteractivemode" data-raw-source="[&lt;strong&gt;SetupSetNonInteractiveMode&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupsetnoninteractivemode)"><strong>SetupSetNonInteractiveMode</strong></a></p></td>
<td align="left"><p>SetupAPI が呼び出し元のコンテキスト内のユーザーと対話できるかどうかを決定する非対話型 SetupAPI フラグを設定します。</p></td>
</tr>
</tbody>
</table>

 

 

 





