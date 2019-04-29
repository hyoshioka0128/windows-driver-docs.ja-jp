---
title: PdoInitFreeDeviceCreateType2 rule (kmdf)
description: PdoInitFreeDeviceCreateType2 ルールでは、ドライバーをする必要がありますを呼び出さないこと WdfDeviceCreate WdfDeviceInitFree を呼び出した後を指定します。
ms.assetid: 0e5c9a97-7bc9-43c7-8bc7-a252e1a1b3d0
ms.date: 05/21/2018
keywords:
- PdoInitFreeDeviceCreateType2 rule (kmdf)
topic_type:
- apiref
api_name:
- PdoInitFreeDeviceCreateType2
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b1402951a50576e21eeb40e193637a9e5f6d2a45
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384098"
---
# <a name="pdoinitfreedevicecreatetype2-rule-kmdf"></a>PdoInitFreeDeviceCreateType2 rule (kmdf)


PdoInitFreeDeviceCreateType2 ルールでは、ドライバーを呼び出してはならないことを指定します[ **WdfDeviceCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff545926)呼び出した後[ **WdfDeviceInitFree** ](https://msdn.microsoft.com/library/windows/hardware/ff546050).

|              |      |
|--------------|------|
| ドライバー モデル | KMDF |

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>PdoInitFreeDeviceCreateType2</strong>ルール。</p>
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

<a name="applies-to"></a>対象
----------

[**WdfDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff545926)
[**WdfDeviceInitFree**](https://msdn.microsoft.com/library/windows/hardware/ff546050)
[**WdfPdoInitAllocate**](https://msdn.microsoft.com/library/windows/hardware/ff548786)
 

 





