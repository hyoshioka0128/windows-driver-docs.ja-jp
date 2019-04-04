---
title: ForwardedAtBadIrqlFsdAsync ルール (wdm)
description: ForwardedAtBadIrqlFsdAsync ルールを指定、ドライバーで IRQL ディスパッチを保留および PoCallDriver を呼び出す\_レベルに転送される IRP の主要な関数のコードが IRP が次のいずれかでない限り\_MJ\_POWERIRP\_MJ\_READIRP\_MJ\_WRITEIRP\_MJ\_デバイス\_CONTROLIRP\_MJ\_内部\_デバイス\_コントロール。
ms.assetid: 9961AE5F-0B36-4E04-A349-CA0461B3E3DC
ms.date: 05/21/2018
keywords:
- ForwardedAtBadIrqlFsdAsync ルール (wdm)
topic_type:
- apiref
api_name:
- ForwardedAtBadIrqlFsdAsync
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bc8f8485e07802626d3ffa403aaa7749a1063220
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552577"
---
# <a name="forwardedatbadirqlfsdasync-rule-wdm"></a>ForwardedAtBadIrqlFsdAsync ルール (wdm)


**ForwardedAtBadIrqlFsdAsync**ルールでは、ドライバーを呼び出すことを指定します[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)と[ **PoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff559654) IRQL で&lt;ディスパッチ\_レベルに転送される IRP の主な機能コードが、次のいずれかである場合。

-   [**IRP\_MJ\_電源**](https://msdn.microsoft.com/library/windows/hardware/ff550784)
-   [**IRP\_MJ\_READ**](https://msdn.microsoft.com/library/windows/hardware/ff550794)
-   [**IRP\_MJ\_WRITE**](https://msdn.microsoft.com/library/windows/hardware/ff550819)
-   [**IRP\_MJ\_DEVICE\_CONTROL**](https://msdn.microsoft.com/library/windows/hardware/ff550744)
-   [**IRP\_MJ\_内部\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550766)

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>ForwardedAtBadIrqlFsdAsync</strong>ルール。</p>
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

[**IoBuildAsynchronousFsdRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548310)
[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)
[**PoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff559654)
 

 





