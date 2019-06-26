---
title: WmiForward ルール (wdm)
description: WmiForward ルールでは、転送が必要な場合に、ドライバーが WMI のマイナー Irp を転送する必要がありますを指定します。
ms.assetid: c62f37d2-ebd5-4705-9590-d1bf17137802
ms.date: 05/21/2018
keywords:
- WmiForward ルール (wdm)
topic_type:
- apiref
api_name:
- WmiForward
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c1caaa93bfe843fa83df0d0f10a896201e58c149
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393100"
---
# <a name="wmiforward-rule-wdm"></a>WmiForward ルール (wdm)


**WmiForward**ルールでは、ドライバーを転送する必要がありますを指定します[ **WMI マイナー Irp** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/wmi-minor-irps)転送が必要な場合。

具体的には、ドライバーを呼び出すと[ **WmiSystemControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)の値、 *IrpDisposition*パラメーターが**IrpForward**、ドライバーを呼び出す必要があります[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)または[ **PoCallDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver)ディスパッチから戻る前に、IRP を転送するにはルーチンです。

このルールは、バス ドライバーには適用されません。

A *WMI マイナー IRP*は、 [ **IRP\_MJ\_システム\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-system-control) WMI マイナー関数コードで要求します。

WMI のマイナー Irp の処理に関する詳細については、次を参照してください[ **WDM ドライバーの要件を WMI**](https://docs.microsoft.com/windows-hardware/drivers/kernel/wmi-requirements-for-wdm-drivers)、 [ **WMI 要求の処理**](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)、 。[**Windows Management Instrumentation ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)、および[ **WMI ライブラリ サポート ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

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
<td align="left"><p>実行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>を指定し、 <strong>WmiForward</strong>ルール。</p>
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

[**IoAcquireRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioacquireremovelock)
[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)
[**PoCallDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver)参照してください。
--------

[**WDM ドライバーの要件を WMI**](https://docs.microsoft.com/windows-hardware/drivers/kernel/wmi-requirements-for-wdm-drivers)
[**WMI 要求を処理して**](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)
[**WMI ライブラリのサポートルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)
 

 





