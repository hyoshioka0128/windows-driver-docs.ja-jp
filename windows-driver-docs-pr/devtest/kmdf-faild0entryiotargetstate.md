---
title: FailD0EntryIoTargetState ルール (kmdf)
description: FailD0EntryIoTargetState ルールでは、同じコールバックから、EvtDeviceD0Entry が失敗した場合、I/O ターゲット、EvtDeviceD0Entry 内で開始する USB の継続的なリーダーが適切に停止にした取得ことを指定します。
ms.assetid: 7FB616EB-2079-42AE-A724-990EFBF3F84D
ms.date: 05/21/2018
keywords:
- FailD0EntryIoTargetState ルール (kmdf)
topic_type:
- apiref
api_name:
- FailD0EntryIoTargetState
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 991fb8b77a5fccce386683c7260a31c7cc304ba9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350413"
---
# <a name="faild0entryiotargetstate-rule-kmdf"></a>FailD0EntryIoTargetState ルール (kmdf)


**FailD0EntryIoTargetState**ルール内で USB の継続的なリーダー対象が I/O が開始されたことを指定します、 [ *EvtDeviceD0Entry* ](https://msdn.microsoft.com/library/windows/hardware/ff540848)は適切に停止の取得同じコールバックから場合、 *EvtDeviceD0Entry*は失敗します。

ときに[ *EvtDeviceD0Entry* ](https://msdn.microsoft.com/library/windows/hardware/ff540848)コールバック関数が失敗した場合、フレームワークは、ドライバーを実行しない[ *EvtDeviceD0Exit* ](https://msdn.microsoft.com/library/windows/hardware/ff540855)コールバック関数。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>FailD0EntryIoTargetState</strong>ルール。</p>
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

<a name="applies-to"></a>対象
----------

[**WdfIoTargetStart**](https://msdn.microsoft.com/library/windows/hardware/ff548677)
[**WdfIoTargetStop**](https://msdn.microsoft.com/library/windows/hardware/ff548680)
[**WdfUsbTargetPipeConfigContinuousReader** ](https://msdn.microsoft.com/library/windows/hardware/ff551130) 
 [ **WdfUsbTargetPipeGetIoTarget**](https://msdn.microsoft.com/library/windows/hardware/ff551146)
 

 





