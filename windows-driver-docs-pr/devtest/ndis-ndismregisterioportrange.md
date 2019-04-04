---
title: NdisMRegisterIoPortRange ルール (ndis)
description: ミニポート ドライバーでは、NdisMRegisterIoPortRange を呼び出し、MiniportInitializeEx またはミニポートから\_追加\_デバイス関数。 MiniportInitializeEx またはミニポート\_追加\_NdisMRegisterIoPortRange を呼び出す前にデバイスが NdisMSetMiniportAttributes を呼び出す必要があります。
ms.assetid: 74CFCBDB-3044-4447-ABEF-A60BA31C0BE0
ms.date: 05/21/2018
keywords:
- NdisMRegisterIoPortRange ルール (ndis)
topic_type:
- apiref
api_name:
- NdisMRegisterIoPortRange
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: abba4de6b4bfed51ddcb75cd75f1329641f43ebc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556609"
---
# <a name="ndismregisterioportrange-rule-ndis"></a>NdisMRegisterIoPortRange ルール (ndis)


ミニポート ドライバーは呼び出し[ **NdisMRegisterIoPortRange** ](https://msdn.microsoft.com/library/windows/hardware/ff563651)からその[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)またはミニポート\_追加\_デバイス関数。 *MiniportInitializeEx*またはミニポート\_追加\_デバイスを呼び出す必要があります[ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)呼び出す前に**NdisMRegisterIoPortRange**します。

|              |      |
|--------------|------|
| ドライバー モデル | NDIS |

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>NdisMRegisterIoPortRange</strong>ルール。</p>
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

[**NdisMRegisterIoPortRange**](https://msdn.microsoft.com/library/windows/hardware/ff563651)
[**NdisMSetMiniportAttributes**](https://msdn.microsoft.com/library/windows/hardware/ff563672)
 

 





