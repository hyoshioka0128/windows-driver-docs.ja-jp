---
title: WmiComplete ルール (wdm)
description: WmiComplete ルールは、WMI のマイナー IRP を処理するときに、ドライバーを呼び出す IoCompleteRequest DispatchSystemControl ルーチンから戻る前に指定します。
ms.assetid: 3908da96-beb1-4651-b41b-06f849b72000
ms.date: 05/21/2018
keywords:
- WmiComplete ルール (wdm)
topic_type:
- apiref
api_name:
- WmiComplete
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9aef7dd9d57202d496bd0ead971c18b9dc8b05e6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556706"
---
# <a name="wmicomplete-rule-wdm"></a>WmiComplete ルール (wdm)


**WmiComplete**ルール指定を処理するときに、 [ **WMI マイナー IRP**](https://msdn.microsoft.com/library/windows/hardware/ff566361)、ドライバー呼び出し[ **IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343)から戻る前に、 [ **DispatchSystemControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン。

A *WMI マイナー IRP*は、 [ **IRP\_MJ\_システム\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550813) WMI マイナー関数コードで要求します。

WMI のマイナー Irp の処理に関する詳細については、次を参照してください[ **WDM ドライバーの要件を WMI**](https://msdn.microsoft.com/library/windows/hardware/ff566370)、 [ **WMI 要求の処理**](https://msdn.microsoft.com/library/windows/hardware/ff546968)、 。[**Windows Management Instrumentation ルーチン**](https://msdn.microsoft.com/library/windows/hardware/ff565794)、および[ **WMI ライブラリ サポート ルーチン**](https://msdn.microsoft.com/library/windows/hardware/ff566359)します。

WMI データ プロバイダーとして登録されていないドライバーには、[次へ] の下のドライバーに WMI 要求を転送する必要があります。 この操作を確認するため、 [ **WmiForward** ](wdm-wmiforward.md)ルール。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>WmiComplete</strong>ルール。</p>
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

[**IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343)
[**WmiSystemControl** ](https://msdn.microsoft.com/library/windows/hardware/ff565834)も参照してください
--------

[**WmiForward**](wdm-wmiforward.md)
[**WDM ドライバーの要件を WMI**](https://msdn.microsoft.com/library/windows/hardware/ff566370)
[**のWMI要求を処理** ](https://msdn.microsoft.com/library/windows/hardware/ff546968) 
 [ **WMI ライブラリ サポート ルーチン**](https://msdn.microsoft.com/library/windows/hardware/ff566359)
 

 





