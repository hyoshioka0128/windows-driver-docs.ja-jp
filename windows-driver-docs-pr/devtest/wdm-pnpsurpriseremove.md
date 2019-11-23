---
title: PnpSurpriseRemove ルール (wdm)
description: PnpSurpriseRemove 規則は、IRP\_削除要求を\_して IRP\_を処理するときに、ドライバーが IoDeleteDevice または IoDetachDevice を呼び出さないことを指定します。
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
ms.openlocfilehash: 0ea29f7b101cd6264c4df2337dc2a6fe6e5c3036
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839885"
---
# <a name="pnpsurpriseremove-rule-wdm"></a>PnpSurpriseRemove ルール (wdm)


**PnpSurpriseRemove**規則は、 [**IRP\_削除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)要求を\_して IRP\_を処理するときに、ドライバーが Iodeletedevice または IoDetachDevice を呼び出さないことを指定します。

PnP マネージャーは、IRP\_\_を実行して、デバイスが i/o 操作で使用できなくなったこと、およびコンピューターから予期せず削除されたことがあることをドライバーに通知するために、 [**IRP\_削除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)要求を送信します。

-   すべての PnP ドライバーは、予期しない IRP\_を処理し、[**突然\_の削除要求\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)処理する必要があります。
-   IRP\_完了\_驚き\_削除 IRP が成功し、デバイスに対して開いているハンドルがすべて閉じられるまで、ドライバーはデバイスオブジェクトで[**Iodeletedevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodeletedevice)または[**IoDetachDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodetachdevice)を呼び出すことはできません。
-   次に、PnP マネージャーは、デバイススタックに\_デバイスの要求を[**削除\_、IRP\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)を送信します。 Remove IRP に応答して、ドライバーはデバイスオブジェクトをスタックからデタッチし、削除します。

予期しない[ **\_irp\_の削除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)要求に対してドライバーが応答する方法の詳細については、「 [**irp\_の\_突然の削除要求を処理**](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-an-irp-mn-surprise-removal-request)する」を参照してください\_。\_

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>PnpSurpriseRemove</strong>規則を指定します。</p>
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

[**Iodeletedevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodeletedevice)
[**IoDetachDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodetachdevice)関連項目
--------

[**Irp\_の処理\_驚く\_の削除要求を処理**](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-an-irp-mn-surprise-removal-request)し、[検証とコード分析ツールを使用してドライバーを分析](https://docs.microsoft.com/windows-hardware/drivers)し

[**IRP\_\_突然\_削除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)
[**IRP\_\_\_デバイスの削除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)
 

 





