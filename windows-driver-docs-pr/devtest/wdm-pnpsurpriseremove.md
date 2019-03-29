---
title: PnpSurpriseRemove ルール (wdm)
description: PnpSurpriseRemove ルールを指定するドライバーは呼び出しません IoDeleteDevice または IoDetachDevice IRP の処理中に\_MN\_突然\_削除要求。
ms.assetid: 58553c78-04c3-423c-bf68-69d5a8fbfa9b
ms.date: 05/21/2018
keywords:
- PnpSurpriseRemove ルール (wdm)
topic_type:
- apiref
api_name:
- PnpSurpriseRemove
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 51dd1ade28f90753a6ccddb7ab5e21b4dd673524
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582435"
---
# <a name="pnpsurpriseremove-rule-wdm"></a>PnpSurpriseRemove ルール (wdm)


**PnpSurpriseRemove**ルールを指定するドライバーは呼び出しません IoDeleteDevice または IoDetachDevice 処理中に、 [ **IRP\_MN\_突然\_削除**](https://msdn.microsoft.com/library/windows/hardware/ff551760)要求。

PnP マネージャーに送信、 [ **IRP\_MN\_突然\_削除**](https://msdn.microsoft.com/library/windows/hardware/ff551760)要求にデバイスが I/O 操作に使用できるがなくなったこととしているドライバーを通知するにはおそらく予期せずから削除されたコンピューター。

-   すべての PnP ドライバーを処理する必要があります[ **IRP\_MN\_突然\_削除**](https://msdn.microsoft.com/library/windows/hardware/ff551760)要求。
-   ドライバーを呼び出してはならない[ **IoDeleteDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff549083)または[ **IoDetachDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff549087) IRP までのデバイス オブジェクト\_MN\_突然\_IRP の削除は成功し、デバイスにすべての開いているハンドルは閉じられます。
-   PnP マネージャーに送信し、 [ **IRP\_MN\_削除\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551738)デバイス スタックを要求します。 IRP の削除に応答してでは、ドライバーは、スタックからそれらのデバイス オブジェクトをデタッチし、それらを削除します。

ドライバーに対する応答方法の詳細については[ **IRP\_MN\_突然\_削除**](https://msdn.microsoft.com/library/windows/hardware/ff551760)要求を参照してください[**処理IRP\_MN\_突然\_削除要求**](https://msdn.microsoft.com/library/windows/hardware/ff546699)

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>PnpSurpriseRemove</strong>ルール。</p>
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

[**IoDeleteDevice**](https://msdn.microsoft.com/library/windows/hardware/ff549083)
[**IoDetachDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff549087)も参照してください
--------

[**IRP の処理\_MN\_突然\_削除要求**](https://msdn.microsoft.com/library/windows/hardware/ff546699)
[検証とコード分析ツールを使用してドライバーを分析](https://msdn.microsoft.com/windows-drivers/develop/testing_a_driver)
 [ **IRP\_MN\_突然\_削除**](https://msdn.microsoft.com/library/windows/hardware/ff551760)
[**IRP\_MN\_削除\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551738)
 

 





