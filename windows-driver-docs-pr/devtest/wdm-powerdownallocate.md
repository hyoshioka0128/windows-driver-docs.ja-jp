---
title: PowerDownAllocate ルール (wdm)
description: エントリの IRP の処理時に、ドライバーを FDO して FIDO がメモリが割り当てられません PowerDownAllocate ルールで指定\_MN\_設定\_SystemPowerState に移行するに s0 から移動するため POWER 要求 \ S1.S5\ します。
ms.assetid: 01737B5F-C1DF-4012-85F2-E9B7517EA53A
ms.date: 05/21/2018
keywords:
- PowerDownAllocate ルール (wdm)
topic_type:
- apiref
api_name:
- PowerDownAllocate
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 985ebde961b95ba16d6ed41c6a85e857588f03fa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384092"
---
# <a name="powerdownallocate-rule-wdm"></a>PowerDownAllocate ルール (wdm)


**PowerDownAllocate**ルール指定のエントリの IRP の処理時に、ドライバーを FDO して FIDO がメモリが割り当てられません\_MN\_設定\_の電源の要求、 **SystemPowerState**に s0 から遷移\[S1.S5\]します。

このルールは、FDO および FIDO ドライバーのみに適用されます。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>PowerDownAllocate</strong>ルール。</p>
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

[**ExAllocatePoolWithTag**](https://msdn.microsoft.com/library/windows/hardware/ff544520)
[**IoAcquireRemoveLock**](https://msdn.microsoft.com/library/windows/hardware/ff548204)
 

 





