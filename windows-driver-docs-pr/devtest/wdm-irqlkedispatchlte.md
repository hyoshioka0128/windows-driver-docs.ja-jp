---
title: IrqlKeDispatchLte ルール (wdm)
ms.assetid: 425a20ea-c9e3-45f4-a517-6bad9ab0de98
ms.date: 05/21/2018
description: ''
keywords:
- IrqlKeDispatchLte ルール (wdm)
topic_type:
- apiref
api_name:
- IrqlKeDispatchLte
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 368a927303267dff6ae6fa1e8260f2049c9980fb
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917910"
---
# <a name="irqlkedispatchlte-rule-wdm"></a>IrqlKeDispatchLte ルール (wdm)


**IrqlKeDispatchLte**規則は、ドライバーが IRQL = ディスパッチレベルで実行されている場合にのみ、次のカーネルルーチンを呼び出すように指定し &lt; \_ ます。

-   [**KeAcquireSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock)

-   [**KeCancelTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kecanceltimer)

-   [**KeClearEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keclearevent)

-   [**KeFlushIoBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keflushiobuffers)

-   [**KeInitializeDeviceQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializedevicequeue)

-   [**KeInitializeTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializetimer)

-   [**KeInitializeTimerEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializetimerex)

-   [**KePulseEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-kepulseevent)

-   [**KeRaiseIrqlToDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keraiseirqltodpclevel)

-   [**KeReadStateEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereadstateevent)

-   [**KeReadStateTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereadstatetimer)

-   [**KeReleaseMutex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasemutex)

-   [**KeRemoveEntryDeviceQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keremoveentrydevicequeue)

-   [**KeResetEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keresetevent)

-   [**Kesaveflo/Pointstate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesavefloatingpointstate)

-   [**KeSetTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesettimer)

-   [**KeSetTimerEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesettimerex)

**ドライバーモデル: WDM**

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグチェック 0xC4: ドライバー \_検証の \_ 検出 \_ 違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(0x00020011) |

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>IrqlKeDispatchLte</strong>規則を指定します。</p>
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

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">実行時</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">ドライバーの検証ツール</a>を実行し、[ <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking" data-raw-source="[DDI compliance checking](https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking)">DDI 準拠チェック</a>] オプションを選択します。</p></td>
</tr>
</tbody>
</table>

 

<a name="applies-to"></a>適用対象
----------

[**KeAcquireSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock) 
[**KeCancelTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kecanceltimer) 
[**Keclearevent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keclearevent) 
[**Keinitializedevicequeue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializedevicequeue) 
[**Keinitializesemaphore**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializesemaphore) 
[**Keinitializetimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializetimer) 
[**Keinitializetimerex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializetimerex) 
[**KePulseEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-kepulseevent) 
[**KeReadStateEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereadstateevent) 
[**KeReadStateTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereadstatetimer) 
[**KeReleaseMutex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasemutex) 
[**Keremoveentrydevicequeue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keremoveentrydevicequeue) 
[**KeResetEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keresetevent) 
[**Kesaveflo/Pointstate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesavefloatingpointstate) 
[**KeSetTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesettimer) 
[**Kesettimerex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesettimerex)
 

 





