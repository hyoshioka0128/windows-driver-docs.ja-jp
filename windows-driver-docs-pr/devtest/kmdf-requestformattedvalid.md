---
title: RequestFormattedValid ルール (kmdf)
description: RequestFormattedValid ルールでは、ドライバーが、WDF を除く、すべての要求を形式を指定します\_要求\_送信\_オプション\_送信\_AND\_に送信する前に、破棄要求I/O ターゲットの場合。
ms.assetid: b7da37ed-3ca5-472e-a915-82674c9efee3
ms.date: 05/21/2018
keywords:
- RequestFormattedValid ルール (kmdf)
topic_type:
- apiref
api_name:
- RequestFormattedValid
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0bb089a7564ce894d5b1b90eb2ff499587ec664f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362665"
---
# <a name="requestformattedvalid-rule-kmdf"></a>RequestFormattedValid ルール (kmdf)


**RequestFormattedValid**ルールでは、ドライバーが、WDF を除く、すべての要求を形式を指定します\_要求\_送信\_オプション\_送信\_AND\_に I/O のターゲットに送信する前に、破棄要求。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>RequestFormattedValid</strong>ルール。</p>
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
[**WdfRequestFormatRequestUsingCurrentType** ](https://msdn.microsoft.com/library/windows/hardware/ff549955) 
[ **WdfRequestSend**](https://msdn.microsoft.com/library/windows/hardware/ff550027)
[**WdfRequestWdmFormatUsingStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff550036) 
[ **WdfUsbTargetDeviceFormatRequestForControlTransfer**](https://msdn.microsoft.com/library/windows/hardware/ff550082)
[**WdfUsbTargetDeviceFormatRequestForCyclePort** ](https://msdn.microsoft.com/library/windows/hardware/ff550084) 
 [ **WdfUsbTargetDeviceFormatRequestForString** ](https://msdn.microsoft.com/library/windows/hardware/ff550086) 
 [ **WdfUsbTargetDeviceFormatRequestForUrb**](https://msdn.microsoft.com/library/windows/hardware/ff550088)
[**WdfUsbTargetPipeFormatRequestForAbort** ](https://msdn.microsoft.com/library/windows/hardware/ff551132) 
[ **WdfUsbTargetPipeFormatRequestForRead**](https://msdn.microsoft.com/library/windows/hardware/ff551136)
[**WdfUsbTargetPipeFormatRequestForReset**](https://msdn.microsoft.com/library/windows/hardware/ff551138) 
 [ **WdfUsbTargetPipeFormatRequestForUrb** ](https://msdn.microsoft.com/library/windows/hardware/ff551139) 
 [ **WdfUsbTargetPipeFormatRequestForWrite**](https://msdn.microsoft.com/library/windows/hardware/ff551141)
 

 





