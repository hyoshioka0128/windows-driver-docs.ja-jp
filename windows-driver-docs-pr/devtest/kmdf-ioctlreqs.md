---
title: IoctlReqs ルール (kmdf)
description: IoctlReqs ルールでは、IOCTL 要求が不適切な KMDF 要求に渡すことはできないか、デバイス ドライバー インターフェイス (Ddi) を送信することを指定します。
ms.assetid: f13aef5a-61e7-4b99-b86e-e1857de3c2f1
ms.date: 05/21/2018
keywords:
- IoctlReqs ルール (kmdf)
topic_type:
- apiref
api_name:
- IoctlReqs
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9785c34c936bfe0909b96357f60cd2fa0abe29ca
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553198"
---
# <a name="ioctlreqs-rule-kmdf"></a>IoctlReqs ルール (kmdf)


**IoctlReqs**ルールは、IOCTL 要求が不適切な KMDF 要求に渡すことはできないか、デバイス ドライバー インターフェイス (Ddi) を送信することを指定します。

すべての要求に、ドライバーの提示[ *EvtIoDeviceControl* ](https://msdn.microsoft.com/library/windows/hardware/ff541758)イベント コールバック関数の IOCTL リクエストすることが保証されます。 ドライバーの*EvtIoDeviceControl* 、EVT を使用して、関数が宣言された\_WDF\_IO\_キュー\_IO\_デバイス\_制御関数のロールの種類宣言。

これらの IOCTL 要求を送信して、読み取りの送信に固有の次の Ddi ことはできません、書き込み、または IOCTL を要求します。

[**WdfUsbTargetPipeSendUrbSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff551158)、 [ **WdfIoTargetSendReadSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff548669)、 [ **WdfIoTargetSendWriteSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/ff548672)、 [ **WdfIoTargetSendInternalIoctlSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff548656)、 [ **WdfIoTargetSendInternalIoctlOthersSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff548651)、 [ **WdfUsbTargetPipeWriteSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff551163)、 [ **WdfUsbTargetPipeReadSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff551155)

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>IoctlReqs</strong>ルール。</p>
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

[**WdfIoTargetSendInternalIoctlOthersSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff548651)
[**WdfIoTargetSendInternalIoctlSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/ff548656) 
 [ **WdfIoTargetSendReadSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff548669)
[**WdfIoTargetSendWriteSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/ff548672) 
[ **WdfUsbTargetPipeReadSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff551155)
[**WdfUsbTargetPipeSendUrbSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/ff551158)
 [ **WdfUsbTargetPipeWriteSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff551163)








