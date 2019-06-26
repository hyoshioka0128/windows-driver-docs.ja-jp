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
ms.openlocfilehash: 3554e569d6f334ba2846a460bcae5570f9c92e6f
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393664"
---
# <a name="pnpsurpriseremove-rule-wdm"></a>PnpSurpriseRemove ルール (wdm)


**PnpSurpriseRemove**ルールを指定するドライバーは呼び出しません IoDeleteDevice または IoDetachDevice 処理中に、 [ **IRP\_MN\_突然\_削除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)要求。

PnP マネージャーに送信、 [ **IRP\_MN\_突然\_削除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)要求にデバイスが I/O 操作に使用できるがなくなったこととしているドライバーを通知するにはおそらく予期せずから削除されたコンピューター。

-   すべての PnP ドライバーを処理する必要があります[ **IRP\_MN\_突然\_削除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)要求。
-   ドライバーを呼び出してはならない[ **IoDeleteDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iodeletedevice)または[ **IoDetachDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iodetachdevice) IRP までのデバイス オブジェクト\_MN\_突然\_IRP の削除は成功し、デバイスにすべての開いているハンドルは閉じられます。
-   PnP マネージャーに送信し、 [ **IRP\_MN\_削除\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)デバイス スタックを要求します。 IRP の削除に応答してでは、ドライバーは、スタックからそれらのデバイス オブジェクトをデタッチし、それらを削除します。

ドライバーに対する応答方法の詳細については[ **IRP\_MN\_突然\_削除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)要求を参照してください[**処理IRP\_MN\_突然\_削除要求**](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-an-irp-mn-surprise-removal-request)

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
<td align="left"><p>実行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>を指定し、 <strong>PnpSurpriseRemove</strong>ルール。</p>
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

<a name="applies-to"></a>対象
----------

[**IoDeleteDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iodeletedevice)
[**IoDetachDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iodetachdevice)も参照してください
--------

[**IRP の処理\_MN\_突然\_削除要求**](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-an-irp-mn-surprise-removal-request)
[検証とコード分析ツールを使用してドライバーを分析](https://docs.microsoft.com/windows-hardware/drivers)
 [ **IRP\_MN\_突然\_削除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)
[**IRP\_MN\_削除\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)
 

 





