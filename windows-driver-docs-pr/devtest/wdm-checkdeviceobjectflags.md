---
title: CheckDeviceObjectFlags ルール (wdm)
description: CheckDeviceObjectFlags ルールでは、バス ドライバーがデバイス オブジェクトが操作のフラグを設定を確認する必要がありますように指定します\_POWER\_PAGABLE およびでは、\_POWER\_FDO と子 Pdo 突入が一貫して設定します。 このルールは、バス ドライバーのみに適用されます。
ms.assetid: E229D3A2-30CE-433A-9889-F762CA923803
ms.date: 05/21/2018
keywords:
- CheckDeviceObjectFlags ルール (wdm)
topic_type:
- apiref
api_name:
- CheckDeviceObjectFlags
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1d9a128344c05ca3289b90b250a24210d4b588e3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530795"
---
# <a name="checkdeviceobjectflags-rule-wdm"></a>CheckDeviceObjectFlags ルール (wdm)


**CheckDeviceObjectFlags**ルールでは、バス ドライバーがデバイス オブジェクトが操作のフラグを設定を確認する必要がありますように指定します\_POWER\_PAGABLE およびでは、\_POWER\_突入が一貫して設定FDO と子の Pdo を行います。 このルールは、バス ドライバーのみに適用されます。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>CheckDeviceObjectFlags</strong>ルール。</p>
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

<a name="applies-to"></a>適用対象
----------

[**Exallocatepoolwithtag に**](https://msdn.microsoft.com/library/windows/hardware/ff544520)
[**IoCreateDevice**](https://msdn.microsoft.com/library/windows/hardware/ff548397)
 

 





