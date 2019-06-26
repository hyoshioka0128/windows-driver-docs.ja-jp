---
title: InternalIoctlReqs ルール (kmdf)
description: InternalIoctlReqs ルールでは、不適切な KMDF 要求送信デバイス ドライバー インターフェイス (Ddi) に内部の IOCTL 要求が渡されないことを指定します。
ms.assetid: a6d75752-21eb-486b-b73a-8d810b392e6b
ms.date: 05/21/2018
keywords:
- InternalIoctlReqs ルール (kmdf)
topic_type:
- apiref
api_name:
- InternalIoctlReqs
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4594e855e61308e8415538951ef243c93e038b1f
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391691"
---
# <a name="internalioctlreqs-rule-kmdf"></a>InternalIoctlReqs ルール (kmdf)


**InternalIoctlReqs**ルールでは、内部 IOCTL 要求は不適切な KMDF 要求送信デバイス ドライバー インターフェイス (Ddi) に渡されませんしていることを指定します。

ドライバー、EVT に表示されるすべての要求\_WDF\_IO\_キュー\_IO\_内部\_デバイス\_コントロールのコールバック関数内部の IOCTL にすることが保証されます要求します。 そのため、読み取り、書き込み、または IOCTL、要求の送信などに固有の Ddi を使用してこれらの Ioctl を送信できません**WdfIoTargetSendReadSynchronously**、 **WdfIoTargetSendWriteSynchronously**、**WdfIoTargetSendIoctlSynchronously**、 **WdfUsbTargetPipeWriteSynchronously**します。

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
<td align="left"><p>実行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>を指定し、 <strong>InternalIoctlReqs</strong>ルール。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">(ロールの型宣言の使用)、コードを準備します。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">Static Driver Verifier を実行します。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">表示し、結果を分析します。</a></li>
</ol>
<p>詳細については、次を参照してください。<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">ドライバーで障害を検出する Static Driver Verifier を使用して</a>します。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>適用対象
----------

[**WdfIoTargetSendIoctlSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetsendioctlsynchronously)
[**WdfIoTargetSendReadSynchronously** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetsendreadsynchronously) 
 [ **WdfIoTargetSendWriteSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetsendwritesynchronously)
[**WdfUsbTargetPipeReadSynchronously** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipereadsynchronously) 
 [ **WdfUsbTargetPipeWriteSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipewritesynchronously)
 

 





