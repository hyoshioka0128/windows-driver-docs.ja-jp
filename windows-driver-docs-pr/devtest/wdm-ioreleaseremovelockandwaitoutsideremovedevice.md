---
title: IoReleaseRemoveLockAndWaitOutsideRemoveDevice ルール (wdm)
description: IoReleaseRemoveLockAndWaitOutsideRemoveDevice ルールで指定する IoReleaseRemoveLockAndWait 呼び出さないで外部 IRP\_MJ\_PNP IRP の\_MN\_削除\_の PnP デバイスドライバー。
ms.assetid: 5787B14D-1793-4B39-A569-9A1308257A26
ms.date: 05/21/2018
keywords:
- IoReleaseRemoveLockAndWaitOutsideRemoveDevice ルール (wdm)
topic_type:
- apiref
api_name:
- IoReleaseRemoveLockAndWaitOutsideRemoveDevice
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4dd594c590b50994bf6799b139bcf24ecbebca55
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574237"
---
# <a name="ioreleaseremovelockandwaitoutsideremovedevice-rule-wdm"></a>IoReleaseRemoveLockAndWaitOutsideRemoveDevice ルール (wdm)


**IoReleaseRemoveLockAndWaitOutsideRemoveDevice**ルールを指定する[ **IoReleaseRemoveLockAndWait** ](https://msdn.microsoft.com/library/windows/hardware/ff549567)呼び出さないで外部 IRP\_MJ\_PNP IRP の\_MN\_削除\_PnP ドライバーのデバイス。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>IoReleaseRemoveLockAndWaitOutsideRemoveDevice</strong>ルール。</p>
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

<a name="applies-to"></a>対象
----------

[**IoReleaseRemoveLockAndWait** ](https://msdn.microsoft.com/library/windows/hardware/ff549567)も参照してください
--------

[削除ロックを使用します。](https://msdn.microsoft.com/library/windows/hardware/ff565504)
 

 





