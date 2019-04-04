---
title: SyncReqSend ルール (kmdf)
description: SyncReqSend ルールでは、同期固有 KMDF デバイス ドライバー インターフェイス メソッドを使用してすべての同期送信要求が行われることと、メソッドがある、0 以外の場合のタイムアウト値の設定を指定します。
ms.assetid: 74d6536e-b5b9-4773-9059-b2cb2e7b474d
ms.date: 05/21/2018
keywords:
- SyncReqSend ルール (kmdf)
topic_type:
- apiref
api_name:
- SyncReqSend
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3773b1f412cca9f48f8418a8072abaaa3a6825c3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559275"
---
# <a name="syncreqsend-rule-kmdf"></a>SyncReqSend ルール (kmdf)


**SyncReqSend**ルールは、同期固有 KMDF デバイス ドライバー インターフェイス メソッドを使用してすべての同期送信要求が行われることと、メソッドがある、0 以外の場合のタイムアウト値の設定を指定します。

ドライバーを呼び出す場合、 *WDFxxxSendXXXSynchronously*ハードウェアがすぐに応答しない場合、スレッド、有効なタイムアウトを設定せずにメソッドを停止になることができます。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>SyncReqSend</strong>ルール。</p>
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

[**WdfIoTargetSendIoctlSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff548660)
[**WdfIoTargetSendReadSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/ff548669) 
 [ **WdfIoTargetSendWriteSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff548672)
[**WdfUsbTargetDeviceSendControlTransferSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/ff550104) 
 [**WdfUsbTargetDeviceSendUrbSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff550105)
[**WdfUsbTargetPipeReadSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/ff551155) 
[ **WdfUsbTargetPipeSendUrbSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff551158)
[**WdfUsbTargetPipeWriteSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff551163)
 

 





