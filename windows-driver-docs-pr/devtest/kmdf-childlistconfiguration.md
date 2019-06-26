---
title: ChildListConfiguration ルール (kmdf)
description: ChildListConfiguration ルールでは、動的な列挙をサポートするドライバーが WdfDeviceCreate 関数を呼び出す前に WdfFdoInitSetDefaultChildListConfig を呼び出す必要がありますを指定します。
ms.assetid: B6A6A775-F2FC-4E73-9B4A-D29BF8CCB649
ms.date: 05/21/2018
keywords:
- ChildListConfiguration ルール (kmdf)
topic_type:
- apiref
api_name:
- ChildListConfiguration
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f6ee12fb4a504dfe9c452cffbfc6180d2363a4da
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391687"
---
# <a name="childlistconfiguration-rule-kmdf"></a>ChildListConfiguration ルール (kmdf)


**ChildListConfiguration**ルールを指定するドライバーをサポートする[動的列挙](https://docs.microsoft.com/windows-hardware/drivers/wdf/dynamic-enumeration)呼び出す必要があります[ **WdfFdoInitSetDefaultChildListConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoinitsetdefaultchildlistconfig)呼び出す前に、 [ **WdfDeviceCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)関数。

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
<td align="left"><p>実行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>を指定し、 <strong>ChildListConfiguration</strong>ルール。</p>
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

[**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)
[**WdfFdoInitSetDefaultChildListConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoinitsetdefaultchildlistconfig)
 

 





