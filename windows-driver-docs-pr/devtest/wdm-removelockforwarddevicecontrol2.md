---
title: RemoveLockForwardDeviceControl2 ルール (wdm)
description: RemoveLockForwardDeviceControl2 ルールは、ドライバーは IRP を別のデバイスを転送する保留を使用する場合に IoAcquireRemoveLock および IoReleaseRemoveLock への呼び出しが正しく使用するかを確認します。
ms.assetid: 4BC5E149-5D5A-4421-9CD2-0CB95276950A
ms.date: 05/21/2018
keywords:
- RemoveLockForwardDeviceControl2 ルール (wdm)
topic_type:
- apiref
api_name:
- RemoveLockForwardDeviceControl2
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 39e7054866b266f798a01926cd650eac9ef72108
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527247"
---
# <a name="removelockforwarddevicecontrol2-rule-wdm"></a>RemoveLockForwardDeviceControl2 ルール (wdm)


**RemoveLockForwardDeviceControl2**への呼び出し規則を確認します[ **IoAcquireRemoveLock** ](https://msdn.microsoft.com/library/windows/hardware/ff548204)と[ **IoReleaseRemoveLock**](https://msdn.microsoft.com/library/windows/hardware/ff549560)ドライバーを使用する場合が正しく使用[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336) IRP を別のデバイスを転送します。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>RemoveLockForwardDeviceControl2</strong>ルール。</p>
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
[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)
[**IoCsqInsertIrp**](https://msdn.microsoft.com/library/windows/hardware/ff549066) 
 [ **IoCsqInsertIrpEx**](https://msdn.microsoft.com/library/windows/hardware/ff549067)
[**IoReleaseRemoveLock** ](https://msdn.microsoft.com/library/windows/hardware/ff549560)
 [ **PoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff559654)
[**RemoveHeadList**](https://msdn.microsoft.com/library/windows/hardware/ff561032)
 

 





