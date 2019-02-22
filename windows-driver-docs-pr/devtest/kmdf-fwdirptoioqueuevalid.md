---
title: FwdIrpToIoQueueValid ルール (kmdf)
description: FwdIrpToIoQueueValid ルールでは、ドライバーが IRP を EvtDeviceWdmIrpDispatch コールバックまたは EvtDeviceWdmIrpPreprocess コールバックのいずれかから WdfDeviceWdmDispatchIrpToIoQueue メソッドを使用して、I/O キューに送信するを指定します。
ms.assetid: 338A1577-AD16-4632-BD8D-C9FDBC4FCDBD
ms.date: 05/21/2018
keywords:
- FwdIrpToIoQueueValid ルール (kmdf)
topic_type:
- apiref
api_name:
- FwdIrpToIoQueueValid
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 62dbc3ca0c9138e494f2265d17ba78e7e11151c6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557126"
---
# <a name="fwdirptoioqueuevalid-rule-kmdf"></a>FwdIrpToIoQueueValid ルール (kmdf)


ルール**FwdIrpToIoQueueValid** 、I/O をドライバーが IRP を送信することを指定しますキューを使用して[ **WdfDeviceWdmDispatchIrpToIoQueue** ](https://msdn.microsoft.com/library/windows/hardware/hh451105)からいずれか、メソッド。[*EvtDeviceWdmIrpDispatch* ](https://msdn.microsoft.com/library/windows/hardware/hh406404)コールバックまたは[ *EvtDeviceWdmIrpPreprocess* ](https://msdn.microsoft.com/library/windows/hardware/ff540925)コールバック。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>FwdIrpToIoQueueValid</strong>ルール。</p>
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

[**WdfDeviceWdmDispatchIrpToIoQueue**](https://msdn.microsoft.com/library/windows/hardware/hh451105)
 

 





