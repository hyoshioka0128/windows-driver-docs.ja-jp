---
title: DoubleComplete rule (ndis)
description: DoubleComplete 規則は、NDIS ドライバーがオブジェクト識別子 (OID) 要求を複数回完了できないことを指定します。
ms.assetid: b79aaf92-3536-4409-ac8d-420a5999409c
ms.date: 05/21/2018
keywords:
- DoubleComplete rule (ndis)
topic_type:
- apiref
api_name:
- DoubleComplete
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fba082fb48123d34f6913ec170c9910e22f9acfa
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917914"
---
# <a name="doublecomplete-rule-ndis"></a>DoubleComplete rule (ndis)


DoubleComplete 規則は、NDIS ドライバーがオブジェクト識別子 (OID) 要求を複数回完了できないことを指定します。

このルールは、 **Miniportoidrequest**コールバック関数から NDIS ステータス SUCCESS が返された場合に、 \_ \_ その要求に対して**NdisMOidRequestComplete**関数を呼び出さないことを確認します。 また、このルールでは、 **Miniportoidrequest**が pending status を返したときに、ドライバーが**NdisMOidRequestComplete**関数をその要求に対して複数回呼び出すことができないように指定しています。

**ドライバーモデル: NDIS**

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>DoubleComplete</strong>規則を指定します。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">コードを準備します (役割の種類の宣言を使います)。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">静的ドライバー検証ツールを実行します。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">結果を表示して分析します。</a></li>
</ol>
<p>詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">Static Driver Verifier を使用したドライバーの欠陥の検出</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>適用対象
----------

[**NdisMOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)
 

 





