---
title: WriteReqs ルール (kmdf)
description: WriteReqs ルールでは、書き込み要求が不適切な KMDF メソッドに渡されないことを指定します。
ms.assetid: 8f5718ec-ab3a-4e4f-8401-9113bf0d9552
ms.date: 05/21/2018
keywords:
- WriteReqs ルール (kmdf)
topic_type:
- apiref
api_name:
- WriteReqs
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c8163c6de17d7ce85f0b5102a891259e20cc3710
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557520"
---
# <a name="writereqs-rule-kmdf"></a>WriteReqs ルール (kmdf)


**WriteReqs**ルールでは、書き込み要求が不適切な KMDF メソッドに渡されないことを指定します。

ドライバーに表示されるすべての要求、 [ *EvtIoWrite* ](https://msdn.microsoft.com/library/windows/hardware/ff541813)イベント コールバック関数のコールバックに要求を記述することが保証されます。 具体的には読み取りまたは IOCTL 要求を送信するように設計された KMDF メソッドを使用して、これらの要求を送信できません。

次のメソッドに、書き込み要求を送信できません。

[**WdfUsbTargetPipeReadSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff551155)

[**WdfIoTargetSendIoctlSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff548660),

[**WdfIoTargetSendInternalIoctlSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff548656),

[**WdfIoTargetSendInternalIoctlOthersSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff548651)、

[**WdfIoTargetSendReadSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff548669)します。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>WriteReqs</strong>ルール。</p>
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
 [ **WdfIoTargetSendIoctlSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff548660)
[**WdfIoTargetSendReadSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/ff548669) 
[ **WdfUsbTargetPipeReadSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff551155)
 

 





