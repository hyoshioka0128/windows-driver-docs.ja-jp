---
title: RemoveLockForwardDeviceControlInternal2 ルール (wdm)
description: IoAcquireRemoveLock および IoReleaseRemoveLock への呼び出しが使用されることで正しく保留を使用して、別のデバイスに IRP を転送するときに、RemoveLockForwardDeviceControlInternal2 ルールを確認します。
ms.assetid: 5EB9E1C5-1AE6-4A03-BC50-BE1117DAB13E
ms.date: 05/21/2018
keywords:
- RemoveLockForwardDeviceControlInternal2 ルール (wdm)
topic_type:
- apiref
api_name:
- RemoveLockForwardDeviceControlInternal2
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c0f910d85b503f028ee9fe6b70f59d87c1baa033
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341570"
---
# <a name="removelockforwarddevicecontrolinternal2-rule-wdm"></a>RemoveLockForwardDeviceControlInternal2 ルール (wdm)


**RemoveLockForwardDeviceControlInternal2**への呼び出し規則を確認します[ **IoAcquireRemoveLock** ](https://msdn.microsoft.com/library/windows/hardware/ff548204)と[ **IoReleaseRemoveLock** ](https://msdn.microsoft.com/library/windows/hardware/ff549560)がで正しく使用 IRP を使用して、転送するときに[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)別のデバイスにします。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>RemoveLockForwardDeviceControlInternal2</strong>ルール。</p>
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
 

 





