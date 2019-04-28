---
title: StorPortDeprecated ルール (storport)
description: このルールは呼び出さないことをドライバーはこれらのいずれかを検証ルーチン StorPortValidateRange または StorPortLogError 非推奨とされます。
ms.assetid: 90223719-91AB-4D10-88A0-0DBD2D99C5B2
ms.date: 05/21/2018
keywords:
- StorPortDeprecated ルール (storport)
topic_type:
- apiref
api_name:
- StorPortDeprecated
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f5dc8f29ea293def1436f2d795dafb2a7b06c2dd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362658"
---
# <a name="storportdeprecated-rule-storport"></a>StorPortDeprecated ルール (storport)


このルールは、ドライバーは呼び出さないことこれらの非推奨のルーチンのいずれかを確認します。**StorPortValidateRange**または**StorPortLogError**します。

|              |          |
|--------------|----------|
| ドライバー モデル | Storport |

<a name="how-to-test"></a>テスト方法
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コンパイル時</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>StorPortDeprecated</strong>ルール。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code)">(ロールの型宣言の使用)、コードを準備します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier)">Static Driver Verifier を実行します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results)">表示し、結果を分析します。</a></li>
</ol>
<p>詳細については、次を参照してください。<a href="https://msdn.microsoft.com/library/windows/hardware/hh454281" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://msdn.microsoft.com/library/windows/hardware/hh454281)">ドライバーで障害を検出する Static Driver Verifier を使用して</a>します。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>適用対象
----------

[**StorPortLogError**](https://msdn.microsoft.com/library/windows/hardware/ff567426)
[**StorPortValidateRange**](https://msdn.microsoft.com/library/windows/hardware/ff567513)
 

 





