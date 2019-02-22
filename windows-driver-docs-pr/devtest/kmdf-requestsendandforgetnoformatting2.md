---
title: RequestSendAndForgetNoFormatting2 ルール (kmdf)
description: RequestSendAndForgetNoFormatting2 ルールは、ドライバーが WDF の送信オプションを使用して I/O ターゲットに送信する前に関数の書式設定、I/O ターゲットを使用して、要求の書式を設定しないことを確認します\_要求\_送信\_オプション。\_送信\_AND\_破棄します。
ms.assetid: 1F50CCE7-62A2-44BB-B7B2-86A7AE8EC4CB
ms.date: 05/21/2018
keywords:
- RequestSendAndForgetNoFormatting2 ルール (kmdf)
topic_type:
- apiref
api_name:
- RequestSendAndForgetNoFormatting2
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5b8facb50ac3980555577dabbd295b1e8a4a3837
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551865"
---
# <a name="requestsendandforgetnoformatting2-rule-kmdf"></a>RequestSendAndForgetNoFormatting2 ルール (kmdf)


**RequestSendAndForgetNoFormatting2**ルールは、ドライバーが WDF の送信オプションを使用して I/O ターゲットに送信する前に関数の書式設定、I/O ターゲットを使用して、要求の書式を設定しないことを確認します\_要求\_。送信\_オプション\_送信\_AND\_破棄します。

**RequestSendAndForgetNoFormatting2**具体的には、ドライバーの作成-要求チェックの規則。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>RequestSendAndForgetNoFormatting2</strong>ルール。</p>
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

[**WdfIoTargetFormatRequestForInternalIoctl**](https://msdn.microsoft.com/library/windows/hardware/ff548595)
[**WdfIoTargetFormatRequestForInternalIoctlOthers** ](https://msdn.microsoft.com/library/windows/hardware/ff548599) 
 [**WdfIoTargetFormatRequestForIoctl**](https://msdn.microsoft.com/library/windows/hardware/ff548604)
[**WdfIoTargetFormatRequestForRead** ](https://msdn.microsoft.com/library/windows/hardware/ff548612) 
 [**WdfIoTargetFormatRequestForWrite**](https://msdn.microsoft.com/library/windows/hardware/ff548620)
[**WdfRequestCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff549951) 
 [ **WdfRequestSend**](https://msdn.microsoft.com/library/windows/hardware/ff550027)
[**WdfUsbTargetDeviceFormatRequestForControlTransfer** ](https://msdn.microsoft.com/library/windows/hardware/ff550082) 
 [ **WdfUsbTargetDeviceFormatRequestForCyclePort**](https://msdn.microsoft.com/library/windows/hardware/ff550084)
[**WdfUsbTargetDeviceFormatRequestForString** ](https://msdn.microsoft.com/library/windows/hardware/ff550086) 
 [**WdfUsbTargetDeviceFormatRequestForUrb**](https://msdn.microsoft.com/library/windows/hardware/ff550088)
[**WdfUsbTargetPipeFormatRequestForAbort** ](https://msdn.microsoft.com/library/windows/hardware/ff551132) 
 [ **WdfUsbTargetPipeFormatRequestForRead** ](https://msdn.microsoft.com/library/windows/hardware/ff551136) 
 [ **WdfUsbTargetPipeFormatRequestForReset**](https://msdn.microsoft.com/library/windows/hardware/ff551138)
[**WdfUsbTargetPipeFormatRequestForUrb** ](https://msdn.microsoft.com/library/windows/hardware/ff551139) 
 [ **WdfUsbTargetPipeFormatRequestForWrite**](https://msdn.microsoft.com/library/windows/hardware/ff551141)
 

 





