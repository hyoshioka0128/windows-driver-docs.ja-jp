---
title: RequestGetStatusValid ルール (kmdf)
description: RequestGetStatusValid ルール WdfRequestSend にエラーが返されるときに、次の状況のいずれかで要求のある WdfRequestGetStatus を呼び出す必要がありますを指定します。WDF の要求が送信されたときに\_要求\_送信\_オプション\_同期します。
ms.assetid: 9EFC41AB-E5BD-4DE8-8936-E71EA64E5430
ms.date: 05/21/2018
keywords:
- RequestGetStatusValid ルール (kmdf)
topic_type:
- apiref
api_name:
- RequestGetStatusValid
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8ad9f1b287538e8babd5f9a1962f96798465d546
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387065"
---
# <a name="requestgetstatusvalid-rule-kmdf"></a>RequestGetStatusValid ルール (kmdf)


**RequestGetStatusValid**ことを指定するルール[ **WdfRequestGetStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff549974)で、次の状況のいずれかの要求を呼び出す必要があります。

-   ときに[ **WdfRequestSend** ](https://msdn.microsoft.com/library/windows/hardware/ff550027)エラーを返します。
-   WDF の要求が送信されたときに\_要求\_送信\_オプション\_同期します。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>RequestGetStatusValid</strong>ルール。</p>
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

[**WdfRequestGetStatus**](https://msdn.microsoft.com/library/windows/hardware/ff549974)
[**WdfRequestSend**](https://msdn.microsoft.com/library/windows/hardware/ff550027)
 

 





