---
title: RemoveLockReleaseCleanup ルール (wdm)
description: RemoveLockReleaseCleanup ルールでは、厳密な交互に IoAcquireRemoveLock および IoReleaseRemoveLock への呼び出しが使用されることを指定します。
ms.assetid: 410CB79D-ADDC-4308-B12E-151DA3815241
ms.date: 05/21/2018
keywords:
- RemoveLockReleaseCleanup ルール (wdm)
topic_type:
- apiref
api_name:
- RemoveLockReleaseCleanup
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0e35a987d7b7172f54939e3307b7dce4541a7339
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551898"
---
# <a name="removelockreleasecleanup-rule-wdm"></a>RemoveLockReleaseCleanup ルール (wdm)


**RemoveLockReleaseCleanup**への呼び出し規則を指定[ **IoAcquireRemoveLock** ](https://msdn.microsoft.com/library/windows/hardware/ff548204)と[ **IoReleaseRemoveLock**](https://msdn.microsoft.com/library/windows/hardware/ff549560)厳密な代替構成で使用されます。 呼び出しごとに**IoAcquireRemoveLock**に一致する呼び出しがあります。 **IoReleaseRemoveLock**します。 さらに、ディスパッチ ルーチンの最後に、ドライバーがロックを保持しない削除します。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>RemoveLockReleaseCleanup</strong>ルール。</p>
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

[**ExInterlockedInsertHeadList**](https://msdn.microsoft.com/library/windows/hardware/ff545397)
[**ExInterlockedInsertTailList** ](https://msdn.microsoft.com/library/windows/hardware/ff545402) 
 [ **ExInterlockedPushEntryList**](https://msdn.microsoft.com/library/windows/hardware/ff545418)
[**InsertHeadList** ](https://msdn.microsoft.com/library/windows/hardware/ff547820) 
 [ **IoAcquireRemoveLock**](https://msdn.microsoft.com/library/windows/hardware/ff548204)
[**IoCsqInsertIrp**](https://msdn.microsoft.com/library/windows/hardware/ff549066)
[**IoCsqInsertIrpEx**](https://msdn.microsoft.com/library/windows/hardware/ff549067) 
 [ **IoReleaseRemoveLock**](https://msdn.microsoft.com/library/windows/hardware/ff549560)
[**IoReleaseRemoveLockAndWait** ](https://msdn.microsoft.com/library/windows/hardware/ff549567)
 [ **RemoveHeadList**](https://msdn.microsoft.com/library/windows/hardware/ff561032)
 

 





