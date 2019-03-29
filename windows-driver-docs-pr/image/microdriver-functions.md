---
title: マイクロドライバーの機能
description: マイクロドライバーの機能
ms.assetid: 491b954a-8ffa-4899-8c7d-0aee409f4742
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ee0dc57d1b5eaa075e3218c90d22306aea426ef
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574453"
---
# <a name="microdriver-functions"></a>マイクロドライバーの機能





WIA ベッド ドライバーでは、WIA microdriver 関数を呼び出すことによって、WIA サービスから要求に応答します。 これらの関数は、すべてのベンダーから提供された microdriver によって実装する必要があり、次の。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff545248" data-raw-source="[&lt;strong&gt;MicroEntry&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545248)"><strong>MicroEntry</strong></a></p></td>
<td><p>WIA ベッド ドライバーから送信されたコマンドに応答します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff547322" data-raw-source="[&lt;strong&gt;Scan&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547322)"><strong>スキャン</strong></a></p></td>
<td><p>デバイスからデータを読み取り、WIA ベッド ドライバーにデータを返します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548129" data-raw-source="[&lt;strong&gt;SetPixelWindow&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548129)"><strong>SetPixelWindow</strong></a></p></td>
<td><p>スキャンする領域を設定します。</p></td>
</tr>
</tbody>
</table>

 

 

 




