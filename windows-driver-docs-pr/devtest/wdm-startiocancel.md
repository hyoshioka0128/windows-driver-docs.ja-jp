---
title: StartIoCancel ルール (wdm)
description: StartIoCancel ルールでは、ドライバーする必要がありますを呼び出さないこと IoSetStartIoAttributes オブジェクト パラメーター セットを FALSE に IoSetCancelRoutine を非 NULLCancel ルーチンを呼び出す前に指定します。
ms.assetid: 08fde0b1-4f4e-473a-9e07-3b39683a3a1b
ms.date: 05/21/2018
keywords:
- StartIoCancel ルール (wdm)
topic_type:
- apiref
api_name:
- StartIoCancel
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e411d62f87a6b3aefb958095c36b7213148cea54
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67394058"
---
# <a name="startiocancel-rule-wdm"></a>StartIoCancel ルール (wdm)


**StartIoCancel**ルールでは、ドライバーを呼び出してはならないことを指定します[ **IoSetStartIoAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iosetstartioattributes)で、*オブジェクト*パラメーター設定**FALSE**呼び出す前に[ **IoSetCancelRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcancelroutine)以外**NULL** [ **キャンセル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_cancel)ルーチン。

設定、*オブジェクト*パラメーターを**FALSE**登録する前に、 [**キャンセル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_cancel)ルーチンによりキャンセル競合条件。

ため、ドライバーの[**キャンセル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_cancel)ルーチンへの呼び出しを含める必要があります[ **IoReleaseCancelSpinLock** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549550(v=vs.85)) (リリースに、スピンはロックが、I/Oマネージャーを呼び出す前に取得、**キャンセル**ルーチン)、両方にドライバーを検証、 **StartIoCancel**ルールと[ **CancelSpinLock** ](wdm-cancelspinlock.md)ルール。

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
<td align="left"><p>実行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>を指定し、 <strong>StartIoCancel</strong>ルール。</p>
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

[**IoSetCancelRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcancelroutine)
[**IoSetStartIoAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iosetstartioattributes)も参照してください
--------

[**CancelSpinLock**](wdm-cancelspinlock.md)
 

 





