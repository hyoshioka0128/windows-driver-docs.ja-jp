---
title: PnpSameDeviceObject ルール (wdm)
description: PnpSameDeviceObject ルールでは、ドライバーが有効なターゲット デバイスのオブジェクトへのポインターを IoAttachDeviceToDeviceStack を呼び出すことを指定します。
ms.assetid: 9430962c-7430-445b-b598-57ce7f34cd45
ms.date: 05/21/2018
keywords:
- PnpSameDeviceObject ルール (wdm)
topic_type:
- apiref
api_name:
- PnpSameDeviceObject
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fc64c55d488a615b189f69055fe7d567c2e09b55
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67392014"
---
# <a name="pnpsamedeviceobject-rule-wdm"></a>PnpSameDeviceObject ルール (wdm)


**PnpSameDeviceObject**ルールでは、ドライバーを呼び出すことを指定します[ **IoAttachDeviceToDeviceStack** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioattachdevicetodevicestack)有効なターゲット デバイスのオブジェクトへのポインター。

示されるデバイス オブジェクトが標準でない場合、ドライバーはこの規則に違反します。 この規則により、ドライバーは、デバイス スタックを正しくアタッチします。

このルールは、ソース オブジェクトへのポインターの有効性を検証しません。

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
<td align="left"><p>実行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>を指定し、 <strong>PnpSameDeviceObject</strong>ルール。</p>
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

[**IoAttachDeviceToDeviceStack**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioattachdevicetodevicestack)
 

 





