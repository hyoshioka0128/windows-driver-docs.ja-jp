---
title: ポート モニター クライアント DLL 関数
description: ポート モニター クライアント DLL 関数
ms.assetid: 41efab1a-0638-4925-90a2-cf68d2306ca6
keywords:
- ポート モニターを WDK の印刷、関数
- クライアント DLL ポート モニター機能 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dda6642f0ed28e09155320d930974ab1cf9643bb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570768"
---
# <a name="port-monitor-client-dll-functions"></a>ポート モニター クライアント DLL 関数





次の表には、ポート モニター UI の DLL を定義する必要がある関数が一覧表示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>関数名</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>DllEntryPoint</strong></p></td>
<td><p>DLL エントリ ポイントと通常呼ばれる<strong>DllMain</strong>、これは、Microsoft Windows SDK ドキュメントで説明します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff545026" data-raw-source="[&lt;strong&gt;AddPortUI&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545026)"><strong>AddPortUI</strong></a></p></td>
<td><p>ポートを作成し、ダイアログ ボックスを表示して構成情報を取得します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546290" data-raw-source="[&lt;strong&gt;ConfigurePortUI&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546290)"><strong>ConfigurePortUI</strong></a></p></td>
<td><p>以前に追加のポートを構成します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff547432" data-raw-source="[&lt;strong&gt;DeletePortUI&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547432)"><strong>DeletePortUI</strong></a></p></td>
<td><p>ポートを削除します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551608" data-raw-source="[&lt;strong&gt;InitializePrintMonitorUI&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551608)"><strong>InitializePrintMonitorUI</strong></a></p></td>
<td><p>ポート モニター UI の DLL を初期化します。</p></td>
</tr>
</tbody>
</table>

 

 

 




