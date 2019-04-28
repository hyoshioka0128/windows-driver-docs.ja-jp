---
title: ForwardedAtBadIrqlAllocate ルール (wdm)
description: ForwardedAtBadIrqlAllocate ルール呼び出すを指定すること、ドライバーする必要があります保留と PoCallDriver IRQL ディスパッチで\_レベルに転送される IRP の主要な関数のコードが IRP が次のいずれかでない限り\_MJ\_POWERIRP\_MJ\_READIRP\_MJ\_WRITEIRP\_MJ\_デバイス\_CONTROLIRP\_MJ\_内部\_デバイス\_コントロール。
ms.assetid: 74BB8358-AE25-4FF8-BBA7-BF108DC2946C
ms.date: 05/21/2018
keywords:
- ForwardedAtBadIrqlAllocate ルール (wdm)
topic_type:
- apiref
api_name:
- ForwardedAtBadIrqlAllocate
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 36357d3cae4a1cb9884c5f913ef01e8bee27dfa3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363482"
---
# <a name="forwardedatbadirqlallocate-rule-wdm"></a>ForwardedAtBadIrqlAllocate ルール (wdm)


**ForwardedAtBadIrqlAllocate**ルールでは、ドライバーを呼び出す必要がありますを指定します[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)と[ **PoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff559654) IRQL で&lt;ディスパッチ\_レベルに転送される IRP の主な機能コードが、次のいずれかである場合。

-   [**IRP\_MJ\_電源**](https://msdn.microsoft.com/library/windows/hardware/ff550784)
-   [**IRP\_MJ\_READ**](https://msdn.microsoft.com/library/windows/hardware/ff550794)
-   [**IRP\_MJ\_WRITE**](https://msdn.microsoft.com/library/windows/hardware/ff550819)
-   [**IRP\_MJ\_DEVICE\_CONTROL**](https://msdn.microsoft.com/library/windows/hardware/ff550744)
-   [**IRP\_MJ\_内部\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550766)

|              |     |
|--------------|-----|
| ドライバー モデル | WDM |

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>ForwardedAtBadIrqlAllocate</strong>ルール。</p>
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

[**IoAllocateIrp**](https://msdn.microsoft.com/library/windows/hardware/ff548257)
[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)
[**PoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff559654)
 

 





