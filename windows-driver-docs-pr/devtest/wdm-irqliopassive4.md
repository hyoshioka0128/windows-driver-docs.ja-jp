---
title: IrqlIoPassive4 ルール (wdm)
ms.assetid: 2bdfa09d-0777-4eaf-85ff-d5accc0f31de
ms.date: 05/21/2018
description: ''
keywords:
- IrqlIoPassive4 ルール (wdm)
topic_type:
- apiref
api_name:
- IrqlIoPassive4
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5fd43a6c30a323ff0635a61145b998a1658d520f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527726"
---
# <a name="irqliopassive4-rule-wdm"></a>IrqlIoPassive4 ルール (wdm)


**IrqlIoPassive4**ルールでは、IRQL で実行されている場合にのみ、ドライバーが、次のルーチンを呼び出すことを指定します = パッシブ\_レベル。

-   [**IoCreateFile**](https://msdn.microsoft.com/library/windows/hardware/ff548418)

-   [**IoCreateNotificationEvent**](https://msdn.microsoft.com/library/windows/hardware/ff549039)

-   [**IoCreateSymbolicLink**](https://msdn.microsoft.com/library/windows/hardware/ff549043)

-   [**IoCreateSynchronizationEvent**](https://msdn.microsoft.com/library/windows/hardware/ff549045)

-   [**IoCreateUnprotectedSymbolicLink**](https://msdn.microsoft.com/library/windows/hardware/ff549050)

-   [**IoDeassignArcName**](https://msdn.microsoft.com/library/windows/hardware/ff549076)

-   [**IoDeleteController**](https://msdn.microsoft.com/library/windows/hardware/ff549078)

-   [**IoDeleteSymbolicLink**](https://msdn.microsoft.com/library/windows/hardware/ff549085)

-   [**IoDisconnectInterrupt**](https://msdn.microsoft.com/library/windows/hardware/ff549089)

|              |     |
|--------------|-----|
| ドライバー モデル | WDM |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x0002000D) |

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>IrqlIoPassive4</strong>ルール。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code)">(ロールの型宣言の使用)、コードを準備します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier)">Static Driver Verifier を実行します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results)">表示し、結果を分析します。</a></li>
</ol>
<p>詳細については、<a href="https://msdn.microsoft.com/library/windows/hardware/hh454281" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://msdn.microsoft.com/library/windows/hardware/hh454281)">ドライバーで障害を検出する Static Driver Verifier を使用して</a>を参照してください。</p></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">実行時に</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff545448" data-raw-source="[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)">Driver Verifier</a>を選択し、 <a href="https://msdn.microsoft.com/library/windows/hardware/hh454208" data-raw-source="[DDI compliance checking](https://msdn.microsoft.com/library/windows/hardware/hh454208)">DDI 準拠の検査</a>オプション。</p></td>
</tr>
</tbody>
</table>

 

<a name="applies-to"></a>適用対象
----------

[**IoCreateFile**](https://msdn.microsoft.com/library/windows/hardware/ff548418)
[**IoCreateNotificationEvent**](https://msdn.microsoft.com/library/windows/hardware/ff549039)
[**IoCreateSynchronizationEvent**](https://msdn.microsoft.com/library/windows/hardware/ff549045) 
 [ **IoCreateUnprotectedSymbolicLink**](https://msdn.microsoft.com/library/windows/hardware/ff549050)
[**IoDeleteController** ](https://msdn.microsoft.com/library/windows/hardware/ff549078)
 [ **IoDeleteSymbolicLink**](https://msdn.microsoft.com/library/windows/hardware/ff549085)
[**IoDisconnectInterrupt**](https://msdn.microsoft.com/library/windows/hardware/ff549089)
 

 





