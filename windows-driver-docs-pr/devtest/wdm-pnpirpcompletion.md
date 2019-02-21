---
title: PnpIrpCompletion ルール (wdm)
description: PnpIrpCompletion ルールは、下位のドライバーを FDO ドライバーが PnP Irp を渡すことを確認します。
ms.assetid: 32b2ed2c-4222-4d93-8323-3ad442a14d9d
ms.date: 05/21/2018
keywords:
- PnpIrpCompletion ルール (wdm)
topic_type:
- apiref
api_name:
- PnpIrpCompletion
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4e1367a65d3a8c87cde38ae68c9133846e39d84c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537193"
---
# <a name="pnpirpcompletion-rule-wdm"></a>PnpIrpCompletion ルール (wdm)


**PnpIrpCompletion**ルールは、FDO ドライバーが下位のドライバーを PnP Irp を渡すことを確認します。

このルールは、バス ドライバーには適用されません。

次の PnP Irp はこの規則から除外されます。

-   IRP\_MN\_クエリ\_インターフェイス
-   IRP\_MN\_クエリ\_停止\_デバイス
-   IRP\_MN\_クエリ\_削除\_デバイス

|              |     |
|--------------|-----|
| ドライバー モデル | WDM |

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>PnpIrpCompletion</strong>ルール。</p>
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

[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)
[**IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343)
[**IoForwardIrpSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/ff549100) 
 [ **PoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff559654)
 

 





