---
title: PnpSurpriseRemove ルール (wdm)
description: PnpSurpriseRemove 規則は、IRP の突然の削除要求の処理中に、ドライバーが IoDeleteDevice または IoDetachDevice を呼び出さないことを指定し \_ \_ \_ ます。
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
ms.openlocfilehash: 06d84d85f5cda055ec444b45eda1bf3e2f2d663e
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917666"
---
# <a name="pnpsurpriseremove-rule-wdm"></a>PnpSurpriseRemove ルール (wdm)


**PnpSurpriseRemove**規則は、 [**IRP の突然の \_ \_ \_ 削除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)要求の処理中に、ドライバーが iodeletedevice または IoDetachDevice を呼び出さないことを指定します。

PnP マネージャーは、 [**IRP の \_ 突然 \_ の \_ 削除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)要求を送信して、デバイスが i/o 操作で使用できなくなったこと、およびコンピューターから予期せず削除されたことをドライバーに通知します。

-   すべての PnP ドライバーは、 [**IRP の \_ 突然の \_ \_ 削除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)要求を処理する必要があります。
-   IRP の突然の[**IoDetachDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodetachdevice)削除 irp が成功し、デバイスに対して開いているハンドルがすべて閉じられるまで、ドライバーはデバイスオブジェクトで[**iodeletedevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodeletedevice)または IoDetachDevice を呼び出すことはできません \_ \_ \_ 。
-   次に、PnP マネージャーが、デバイススタックに IRP の " [** \_ \_ \_ デバイスの削除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)" 要求を送信します。 Remove IRP に応答して、ドライバーはデバイスオブジェクトをスタックからデタッチし、削除します。

ドライバーが[**irp の \_ 突然の \_ \_ 削除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)要求に応答する方法の詳細については、「 [**irp の突然の \_ \_ \_ 削除要求の処理**](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-an-irp-mn-surprise-removal-request)」を参照してください。

**ドライバーモデル: WDM**

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>PnpSurpriseRemove</strong>規則を指定します。</p>
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

[**Iodeletedevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodeletedevice) 
[**IoDetachDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodetachdevice)関連項目
--------

[**IRP \_ の処理\_ \_ **](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-an-irp-mn-surprise-removal-request) 
 [確認とコード分析ツールを使用したドライバーの分析による](https://docs.microsoft.com/windows-hardware/drivers)驚くほどの削除要求 
 [**irp の \_ \_ 突然 \_ **](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)の削除 
 [**irp の削除、 \_ \_ \_ デバイスの削除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)
 

 





