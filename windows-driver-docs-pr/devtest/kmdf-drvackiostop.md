---
title: DrvAckIoStop ルール (kmdf)
description: ドライバーがある保留中の要求の対応、電源管理対象のキューを完了すると、または、保留中の要求を取り消しますが承認されると、ドライバーと電源の切断を取得するには、それに応じて DrvAckIoStop ルールを確認します。
ms.assetid: 4C6F8919-C3DF-4DE2-94EF-45475CE9E0C0
ms.date: 05/21/2018
keywords:
- DrvAckIoStop ルール (kmdf)
topic_type:
- apiref
api_name:
- DrvAckIoStop
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d199d9e30953ff276e9c6ebfc84cd86a14e43def
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536224"
---
# <a name="drvackiostop-rule-kmdf"></a>DrvAckIoStop ルール (kmdf)


**DrvAckIoStop**ルールは、電源管理対象のキューが電源の切断を取得して、ドライバーの確認が完了したら、またはそれに応じて保留中の要求をキャンセル中に、ドライバーは保留中の要求を認識を検証します。 自己管理型の I/O 要求の場合、ドライバーも正しくこれらによる要求の処理からその[ *EvtDeviceSelfManagedIoSuspend* ](https://msdn.microsoft.com/library/windows/hardware/ff540907)関数。 電源オフ時にこれらの要求を処理するために失敗したドライバーが引き起こす[ **0x9F のバグ チェック。ドライバー\_POWER\_状態\_エラー**](https://msdn.microsoft.com/library/windows/hardware/ff559329)します。

状況によっては、この警告を抑制する適切な場合があります。 使用することができます、ドライバーには、キューのハンドラーで直接、要求が完了すると、ドライバーは、要求で保持されませんまたはその他のドライバーを転送せず場合、  **\_ \_analysis\_を前提としています**警告を抑制する関数。 詳細については、次を参照してください。[を使用して、 \_analysis\_False 欠陥を抑制する関数を想定しています。](https://msdn.microsoft.com/library/windows/hardware/ff556059)と[**方法。使用して追加のコード情報を指定\_ \_analysis\_想定**](https://msdn.microsoft.com/library/windows/hardware/ms404702)します。

|              |      |
|--------------|------|
| ドライバー モデル | KMDF |

|                                   |                                                                                                          |
|-----------------------------------|----------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**チェック 0x9F バグの。ドライバー\_POWER\_状態\_エラー**](https://msdn.microsoft.com/library/windows/hardware/ff559329) |

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>DrvAckIoStop</strong>ルール。</p>
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

[**WdfDeviceInitSetPnpPowerEventCallbacks**](https://msdn.microsoft.com/library/windows/hardware/ff546135)
[**WdfFdoInitSetFilter**](https://msdn.microsoft.com/library/windows/hardware/ff547273)
[**WdfIoQueueCreate**](https://msdn.microsoft.com/library/windows/hardware/ff547401)
 

 





