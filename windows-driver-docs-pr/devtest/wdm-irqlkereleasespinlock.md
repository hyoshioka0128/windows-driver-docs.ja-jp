---
title: IrqlKeReleaseSpinLock ルール (wdm)
description: IrqlKeReleaseSpinLock ルールでは、IRQL のディスパッチで実行されている場合にのみ、ドライバーが KeReleaseSpinLock を呼び出すことを指定します\_レベル。
ms.assetid: 4abc4010-c653-44ab-9eaa-621d0ed2f354
ms.date: 05/21/2018
keywords:
- IrqlKeReleaseSpinLock ルール (wdm)
topic_type:
- apiref
api_name:
- IrqlKeReleaseSpinLock
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 144417b7e5011a88bb4271bb1fe73d15697b2ed4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573351"
---
# <a name="irqlkereleasespinlock-rule-wdm"></a>IrqlKeReleaseSpinLock ルール (wdm)


**IrqlKeReleaseSpinLock**ルールでは、ドライバーを呼び出すことを指定します[ **KeReleaseSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff553145)のみときに実行されている IRQL でディスパッチを =\_レベル。

このルールも指定する値の*NewIrql*への呼び出しでパラメーター **KeReleaseSpinLock**は、ドライバーが呼び出しの前に実行する IRQL と等しく[ **KeAcquireSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff551917)します。 (この値の値でも、 *OldIrql*パラメーターによって指定された**KeAcquireSpinLock**)。

|              |     |
|--------------|-----|
| ドライバー モデル | WDM |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00020015) |

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>IrqlKeReleaseSpinLock</strong>ルール。</p>
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

[**KeReleaseSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff553145)
 

 





