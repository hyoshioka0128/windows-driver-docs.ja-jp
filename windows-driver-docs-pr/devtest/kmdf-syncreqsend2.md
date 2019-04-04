---
title: SyncReqSend2 ルール (kmdf)
description: SyncReqSend2 ルールでは、同期要求の送信に 0 以外のタイムアウト値が設定を指定します。
ms.assetid: c72b909f-6160-47da-8e7e-84e0dea785c2
ms.date: 05/21/2018
keywords:
- SyncReqSend2 ルール (kmdf)
topic_type:
- apiref
api_name:
- SyncReqSend2
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3f9776cb9b0bda5cd74b9507755acc425c2b5a8c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560792"
---
# <a name="syncreqsend2-rule-kmdf"></a>SyncReqSend2 ルール (kmdf)


**SyncReqSend2**ルールでは、同期要求の送信が 0 以外のタイムアウト値が設定を持つことを指定します。

ドライバーを呼び出す場合[ **WdfRequestSend** ](https://msdn.microsoft.com/library/windows/hardware/ff550027)ハードウェアがすぐに応答しない場合、要求オプションで有効なタイムアウトを設定せず、スレッドを停止することができます。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>SyncReqSend2</strong>ルール。</p>
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

[**WdfRequestSend**](https://msdn.microsoft.com/library/windows/hardware/ff550027)
 

 





