---
title: IrqlPsPassive ルール (wdm)
ms.assetid: db84c945-7695-4691-8294-095bbc74ef8a
ms.date: 05/21/2018
description: ''
keywords:
- IrqlPsPassive ルール (wdm)
topic_type:
- apiref
api_name:
- IrqlPsPassive
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bc2ec9264a890e509a3247c8bffad338fe49b292
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331374"
---
# <a name="irqlpspassive-rule-wdm"></a>IrqlPsPassive ルール (wdm)


**IrqlPsPassive**ルールでは、ドライバーが、次を呼び出すことを指定します[**構造の処理ルーチン**](https://msdn.microsoft.com/library/windows/hardware/ff559917) IRQL でその実行はときにのみ = パッシブ\_レベル:

-   [**PsCreateSystemThread**](https://msdn.microsoft.com/library/windows/hardware/ff559932)

-   [**PsGetVersion**](https://msdn.microsoft.com/library/windows/hardware/ff559941)

-   [**PsSetCreateProcessNotifyRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff559951)

-   [**PsSetCreateThreadNotifyRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff559954)

-   [**PsSetLoadImageNotifyRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff559957)

-   [**PsTerminateSystemThread**](https://msdn.microsoft.com/library/windows/hardware/ff559959)

|              |     |
|--------------|-----|
| ドライバー モデル | WDM |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x0002001C) |

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>IrqlPsPassive</strong>ルール。</p>
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

 

<a name="applies-to"></a>対象
----------

[**PsCreateSystemThread**](https://msdn.microsoft.com/library/windows/hardware/ff559932)
[**PsGetVersion**](https://msdn.microsoft.com/library/windows/hardware/ff559941)
[**PsSetCreateProcessNotifyRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff559951) 
 [ **PsSetCreateThreadNotifyRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff559954)
[**PsSetLoadImageNotifyRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff559957) 
 [ **PsTerminateSystemThread**](https://msdn.microsoft.com/library/windows/hardware/ff559959)
 

 





