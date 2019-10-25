---
title: DanglingDeviceObjectReference ルール (wdm)
description: DanglingDeviceObjectReference 規則は、ドライバーが IoGetAttachedDeviceReference から返されたものと同じデバイスオブジェクトポインターを使用して ObDereferenceObject を呼び出すことを指定します。
ms.assetid: b2aeaa16-f246-48c7-9e80-719d441a44ef
ms.date: 05/21/2018
keywords:
- DanglingDeviceObjectReference ルール (wdm)
topic_type:
- apiref
api_name:
- DanglingDeviceObjectReference
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 507dcce5a984a14b7a2a52bbe0bc4b4813b2b79d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839241"
---
# <a name="danglingdeviceobjectreference-rule-wdm"></a>DanglingDeviceObjectReference ルール (wdm)


**DanglingDeviceObjectReference**規則は、ドライバーが[**IoGetAttachedDeviceReference**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iogetattacheddevicereference)から返されたものと同じデバイスオブジェクトポインターを使用して[**ObDereferenceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject)を呼び出すことを指定します。

このルールは、 **IoGetAttachedDeviceReference**を呼び出してドライバーが参照するすべてのデバイスオブジェクトポインターが、ドライバーが終了する前に**ObDereferenceObject**を呼び出すことによって逆参照されることも指定します。 ObfDereferenceObject

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>DanglingDeviceObjectReference</strong>規則を指定します。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">コードを準備します (ロールの種類の宣言を使用します)。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">静的ドライバー検証ツールを実行します。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">結果を表示して分析します。</a></li>
</ol>
<p>詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">Static Driver Verifier を使用したドライバーの欠陥の検出</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>適用対象
----------

[**IoGetAttachedDeviceReference**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iogetattacheddevicereference)
 

 





