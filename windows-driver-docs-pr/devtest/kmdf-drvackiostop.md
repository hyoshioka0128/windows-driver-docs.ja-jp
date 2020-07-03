---
title: DrvAckIoStop ルール (kmdf)
description: DrvAckIoStop ルールは、ドライバーが保留中の要求を認識しているときに、その電源管理キューの電源が入っていないことを確認します。ドライバーは、それに応じて保留中の要求を確認、完了、またはキャンセルします。
ms.assetid: 4C6F8919-C3DF-4DE2-94EF-45475CE9E0C0
ms.date: 05/21/2018
keywords:
- DrvAckIoStop ルール (kmdf)
topic_type:
- apiref
api_name:
- DrvAckIoStop
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a3f79bb5c05ef8700cc0d0ad7d9ad0ae867ca102
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917952"
---
# <a name="drvackiostop-rule-kmdf"></a>DrvAckIoStop ルール (kmdf)


**DrvAckIoStop**ルールは、ドライバーが保留中の要求を認識しているときに、その電源管理キューの電源が入っていないことを確認します。ドライバーは、それに応じて保留中の要求を確認、完了、またはキャンセルします。 自己管理型の i/o 要求の場合、ドライバーは[*Evtdeviceselfmanagediosuspend*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend)関数からこれらの要求を正しく処理する必要があります。 電源がオフのときにこれらの要求を処理できないドライバーは、バグチェック0x9F を発生させます。[**ドライバーの \_ 電源 \_ 状態が \_ エラー**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0x9f--driver-power-state-failure)になります。

状況によっては、この警告を抑制することが適切な場合があります。 ドライバーが要求を保留していない場合、または他のドライバーに転送しない場合、およびドライバーがキューのハンドラーで要求を直接完了した場合は、 ** \_ \_ 分析を \_ 想定**する関数を使用して警告を非表示にすることができます。 詳細については、「[分析を想定した関数を使用した \_ \_ 誤欠陥の抑制](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-the--analysis-assume-function-to-suppress-false-defects)」と「[**方法: \_ \_ 分析 \_ を使用して追加のコード情報を指定**](https://docs.microsoft.com/visualstudio/code-quality/how-to-specify-additional-code-information-by-using-analysis-assume?view=vs-2015)する」を参照してください。

**ドライバーモデル: KMDF**

|                                   |                                                                                                          |
|-----------------------------------|----------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグチェック 0x9F: ドライバーの \_ 電源 \_ 状態 \_ エラー**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0x9f--driver-power-state-failure) |

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>DrvAckIoStop</strong>規則を指定します。</p>
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

[**WdfDeviceInitSetPnpPowerEventCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpnppowereventcallbacks) 
[**WdfFdoInitSetFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitsetfilter) 
[**WdfIoQueueCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuecreate)
 

 





