---
title: StartIoCancel ルール (wdm)
description: StartIoCancel ルールでは、Null 以外のキャンセルルーチンを使用して Iosetcancelルーチンを呼び出す前に、キャンセル不可能なパラメーターを FALSE に設定して、ドライバーが IoSetStartIoAttributes を呼び出すことができないことを指定します。
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
ms.openlocfilehash: 2b6f7856904595e40848c1df8f52026e6be1c84d
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917846"
---
# <a name="startiocancel-rule-wdm"></a>StartIoCancel ルール (wdm)


**Startiocancel**ルールでは、*非キャンセルのパラメーターを* **FALSE**に設定して、ドライバーが[**iosetstartioattributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iosetstartioattributes)を呼び出してはいけないことを指定します。その前に、**NULL**以外の[**キャンセル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)ルーチンで[**iosetcancelルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcancelroutine)を呼び出します。

キャンセルルーチンを登録する前に[**キャンセル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)不可能なパラメーターを**FALSE**に設定する*と、キャンセル*の競合状態が発生する可能性があります。

ドライバーの[**キャンセル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)ルーチンには[**IoReleaseCancelSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549550(v=vs.85))の呼び出しが含まれている必要があるため (**キャンセル**ルーチンを呼び出す前に i/o マネージャーによって取得されるスピンロックを解除するため)、 **Startiocancel**規則と[**cancelspinlock ロック**](wdm-cancelspinlock.md)規則の両方を使用してドライバーを確認することを検討してください。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>Startiocancel</strong>ルールを指定します。</p>
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

[**Iosetcancelroutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcancelroutine) 
[**Iosetstartioattributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iosetstartioattributes)関連項目
--------

[**CancelSpinLock**](wdm-cancelspinlock.md)
 

 





