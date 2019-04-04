---
title: MarkStartDevice ルール (wdm)
description: MarkStartDevice ルールを指定するドライバーが IRP を保留\_MN\_開始\_デバイス IRP 正しくします。 このルールは、FDO および FIDO ドライバーのみに適用されます。
ms.assetid: ABFE062D-37A7-4931-961C-76092D7C05B7
ms.date: 05/21/2018
keywords:
- MarkStartDevice ルール (wdm)
topic_type:
- apiref
api_name:
- MarkStartDevice
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 77ce08ad2b096462270eb932708d1963145364dd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535613"
---
# <a name="markstartdevice-rule-wdm"></a>MarkStartDevice ルール (wdm)


**MarkStartDevice**ルールを指定するドライバーが IRP を保留\_MN\_開始\_デバイス IRP 正しくします。 このルールは、FDO および FIDO ドライバーのみに適用されます。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>MarkStartDevice</strong>ルール。</p>
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

[**IoAcquireRemoveLock**](https://msdn.microsoft.com/library/windows/hardware/ff548204)
[**IoAllocateIrp**](https://msdn.microsoft.com/library/windows/hardware/ff548257)
[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)
 [ **IoGetDeviceInterfaces**](https://msdn.microsoft.com/library/windows/hardware/ff549186)
[**IoMarkIrpPending** ](https://msdn.microsoft.com/library/windows/hardware/ff549422) 
[ **IoRegisterPlugPlayNotification**](https://msdn.microsoft.com/library/windows/hardware/ff549526)
[**IoSetCompletionRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff549679) 
[ **IoSetCompletionRoutineEx**](https://msdn.microsoft.com/library/windows/hardware/ff549686)
[**PoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff559654)
 

 





