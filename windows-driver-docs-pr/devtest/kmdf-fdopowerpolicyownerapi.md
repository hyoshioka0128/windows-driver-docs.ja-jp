---
title: FDOPowerPolicyOwnerAPI ルール (kmdf)
description: FDOPowerPolicyOwnerAPI ルールの場合は、FDO ドライバーでは、電源ポリシーの所有権を解放、WdfDeviceInitSetPowerPolicyEventCallbacks、WdfDeviceAssignS0IdleSettings、および WdfDeviceAssignSxWakeSettings メソッドのみ呼び出すことができますを指定します、ドライバーの場所が電源ポリシーの所有者の実行パス。 SDV は、この規則の警告を発行します。
ms.assetid: b0695dff-070c-4c55-a71d-a78fc45eb805
ms.date: 05/21/2018
keywords:
- FDOPowerPolicyOwnerAPI ルール (kmdf)
topic_type:
- apiref
api_name:
- FDOPowerPolicyOwnerAPI
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d4d3bb8e4f57344b96e22e4a4d2eaf73751732c9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528602"
---
# <a name="fdopowerpolicyownerapi-rule-kmdf"></a>FDOPowerPolicyOwnerAPI ルール (kmdf)


**FDOPowerPolicyOwnerAPI**規則で指定された場合、メソッド、電源ポリシー所有権を解放する、FDO ドライバー [ **WdfDeviceInitSetPowerPolicyEventCallbacks** ](https://msdn.microsoft.com/library/windows/hardware/ff546774)、 [ **WdfDeviceAssignS0IdleSettings**](https://msdn.microsoft.com/library/windows/hardware/ff545903)、および[ **WdfDeviceAssignSxWakeSettings** ](https://msdn.microsoft.com/library/windows/hardware/ff545909)のみで呼び出すことができます、ドライバーの場所が電源ポリシーの所有者の実行パス。 SDV は、この規則の警告を発行します。

FDO、ドライバーを呼び出す場合、 [ **WdfDeviceInitSetPowerPolicyOwnership** ](https://msdn.microsoft.com/library/windows/hardware/ff546776)メソッド**FALSE** への後続の呼び出し、2番目のパラメーターの値として[ **WdfDeviceInitSetPowerPolicyEventCallbacks**](https://msdn.microsoft.com/library/windows/hardware/ff546774)、 **WdfDeviceAssignS0IdleSettings**、および**WdfDeviceAssignSxWakeSettings**ドライバーでは、規則違反および警告メッセージが発生します。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>FDOPowerPolicyOwnerAPI</strong>ルール。</p>
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

[**WdfDeviceAssignS0IdleSettings**](https://msdn.microsoft.com/library/windows/hardware/ff545903)
[**WdfDeviceAssignSxWakeSettings** ](https://msdn.microsoft.com/library/windows/hardware/ff545909) 
 [ **WdfDeviceInitSetPowerPolicyEventCallbacks**](https://msdn.microsoft.com/library/windows/hardware/ff546774)
[**WdfDeviceInitSetPowerPolicyOwnership**](https://msdn.microsoft.com/library/windows/hardware/ff546776)
 

 





