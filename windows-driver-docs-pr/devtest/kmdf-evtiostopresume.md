---
title: EvtIoStopResume ルール (kmdf)
description: EvtIoStopResume ルールでは、ドライバーは、EvtIoStop コールバック関数を登録し、false Requeue パラメーターと等しいと WdfRequestStopAcknowledge を呼び出し、ドライバーは EvtIoResume コールバック関数を登録する必要があることを指定します。
ms.assetid: 52bcaf8a-545c-4607-89c3-d4474bd50376
ms.date: 05/21/2018
keywords:
- EvtIoStopResume ルール (kmdf)
topic_type:
- apiref
api_name:
- EvtIoStopResume
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0b3d9d22c0df4c9b80b5e8a67b0344bdc464c3ed
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580370"
---
# <a name="evtiostopresume-rule-kmdf"></a>EvtIoStopResume ルール (kmdf)


**EvtIoStopResume**ルール指定する場合は、ドライバーは、登録、 [ *EvtIoStop* ](https://msdn.microsoft.com/library/windows/hardware/ff541788)コールバック関数に呼び出し[ **WdfRequestStopAcknowledge** ](https://msdn.microsoft.com/library/windows/hardware/ff550033)で、*をもう一度キュー*パラメーターと等しい**FALSE**、ドライバーを登録する必要があります、 [ *EvtIoResume* ](https://msdn.microsoft.com/library/windows/hardware/ff541779)コールバック関数。 フレームワークへの要求を提供する、 **EvtIoResume**デバイス D0 状態をもう一度入力するときのコールバック関数。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>EvtIoStopResume</strong>ルール。</p>
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

[**WdfRequestStopAcknowledge**](https://msdn.microsoft.com/library/windows/hardware/ff550033)
 

 





