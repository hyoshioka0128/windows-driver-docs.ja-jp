---
title: LowerDriverReturn ルール (wdm)
description: LowerDriverReturn ルールことを指定します PoCallDriver または保留を使用して、下位のドライバーを呼び出すの後、ドライバー、呼び出しから戻り値の状態を保存します。 ディスパッチ ルーチンに受信した戻り値の状態を渡します。
ms.assetid: 0b437591-c613-481a-a4f9-36a5cc208cb0
ms.date: 05/21/2018
keywords:
- LowerDriverReturn ルール (wdm)
topic_type:
- apiref
api_name:
- LowerDriverReturn
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 14c44a6577aad59822f1fb221f9e1ca65d3ce8ad
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532885"
---
# <a name="lowerdriverreturn-rule-wdm"></a>LowerDriverReturn ルール (wdm)


**LowerDriverReturn**ルールでは、その後の使用を指定します[ **PoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff559654)または[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)下位のドライバーを呼び出すには、ドライバーが呼び出しから戻り値の状態を保存し、ディスパッチ ルーチンに受信した戻り値の状態を渡します。

ドライバーを呼び出す場合、これらの条件が適用されません[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)または[ **IoMarkIrpPending**](https://msdn.microsoft.com/library/windows/hardware/ff549422)します。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>LowerDriverReturn</strong>ルール。</p>
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

[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)
[**IoMarkIrpPending**](https://msdn.microsoft.com/library/windows/hardware/ff549422)
[**IoSetCompletionRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff549679) 
 [ **IoSetCompletionRoutineEx**](https://msdn.microsoft.com/library/windows/hardware/ff549686)
[**IoSetDeviceInterfaceState** ](https://msdn.microsoft.com/library/windows/hardware/ff549700)
 [ **IoWMIRegistrationControl**](https://msdn.microsoft.com/library/windows/hardware/ff550480)
[**kewaitforsingleobject の 1** ](https://msdn.microsoft.com/library/windows/hardware/ff553350) 
[ **PoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff559654)
 

 





