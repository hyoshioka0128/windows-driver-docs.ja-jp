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
ms.openlocfilehash: 143796afedc53640fbacdaa5a0f552d1fd636b6e
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67392000"
---
# <a name="wmicomplete-rule-wdm"></a>WmiComplete ルール (wdm)


**WmiComplete**ルール指定を処理するときに、 [ **WMI マイナー IRP**](https://docs.microsoft.com/windows-hardware/drivers/kernel/wmi-minor-irps)、ドライバー呼び出し[ **IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)から戻る前に、 [ **DispatchSystemControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン。

A *WMI マイナー IRP*は、 [ **IRP\_MJ\_システム\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-system-control) WMI マイナー関数コードで要求します。

WMI のマイナー Irp の処理に関する詳細については、次を参照してください[ **WDM ドライバーの要件を WMI**](https://docs.microsoft.com/windows-hardware/drivers/kernel/wmi-requirements-for-wdm-drivers)、 [ **WMI 要求の処理**](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)、 。[**Windows Management Instrumentation ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)、および[ **WMI ライブラリ サポート ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

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
<td align="left"><p>実行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>を指定し、 <strong>WmiComplete</strong>ルール。</p>
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

[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)
[**WmiSystemControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)も参照してください
--------

[**WmiForward**](wdm-wmiforward.md)
[**WDM ドライバーの要件を WMI**](https://docs.microsoft.com/windows-hardware/drivers/kernel/wmi-requirements-for-wdm-drivers)
[**のWMI要求を処理** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests) 
 [ **WMI ライブラリ サポート ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)
 

 





