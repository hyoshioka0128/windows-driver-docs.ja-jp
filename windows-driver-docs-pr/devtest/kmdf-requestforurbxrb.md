---
title: RequestForUrbXrb ルール (kmdf)
ms.assetid: 8BFFB73D-106A-4CD0-93F2-D295D969729E
ms.date: 05/21/2018
description: ''
keywords:
- RequestForUrbXrb ルール (kmdf)
topic_type:
- apiref
api_name:
- RequestForUrbXrb
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5f860743c2ffe9810321b4ac10e80ba83b21558a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536819"
---
# <a name="requestforurbxrb-rule-kmdf"></a>RequestForUrbXrb ルール (kmdf)


クライアント ドライバーを呼び出す場合[ **WdfUsbTargetDeviceCreateWithParameters** ](https://msdn.microsoft.com/library/windows/hardware/hh439428)とクライアント コントラクト バージョン USBD\_クライアント\_コントラクト\_バージョン\_、WDF の 602\_USB\_デバイス\_作成\_構成構造体の (Windows 8 の USB ドライバー スタックの新機能を使用) する、使用、URB 内部的にのみ使用するDdi*URB コンテキスト*次の前提条件のいずれかに該当する場合。

-   要求パラメーターでは、その親オブジェクトのツリーで、Wdf デバイスがあります。
-   要求は I/O キューを使用して表されます。
-   その親オブジェクトのツリー内の要求が表されるもう 1 つの I/O キューを要求します。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>RequestForUrbXrb</strong>ルール。</p>
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

[**WdfRequestCreate**](https://msdn.microsoft.com/library/windows/hardware/ff549951)
[**WdfUsbTargetDeviceCreateWithParameters** ](https://msdn.microsoft.com/library/windows/hardware/hh439428) 
 [ **WdfUsbTargetDeviceFormatRequestForControlTransfer**](https://msdn.microsoft.com/library/windows/hardware/ff550082)
[**WdfUsbTargetDeviceFormatRequestForString** ](https://msdn.microsoft.com/library/windows/hardware/ff550086) 
[ **WdfUsbTargetDeviceSendControlTransferSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff550104)
[**WdfUsbTargetPipeAbortSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/ff551129)
 [ **WdfUsbTargetPipeFormatRequestForAbort**](https://msdn.microsoft.com/library/windows/hardware/ff551132)
[**WdfUsbTargetPipeFormatRequestForReset** ](https://msdn.microsoft.com/library/windows/hardware/ff551138) 
 [ **WdfUsbTargetPipeResetSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff551156)
 

 





