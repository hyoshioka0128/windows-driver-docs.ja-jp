---
title: RemoveLockMnRemove2 ルール (wdm)
description: RemoveLockMnRemove2 ルールでは、irp が\_に\_処理されたときに、irp が低いドライバーに転送される前に\_デバイスの要求を削除するときに、IoAcquireRemoveLock と IoReleaseRemoveLockAndWait の呼び出しが正しく使用されることを確認します。
ms.assetid: 69CCB0CB-86E0-4994-AC3E-44A4B9993EBC
ms.date: 05/21/2018
keywords:
- RemoveLockMnRemove2 ルール (wdm)
topic_type:
- apiref
api_name:
- RemoveLockMnRemove2
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 50b21cbe846be67a34cafd50645db2814707ae39
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839123"
---
# <a name="removelockmnremove2-rule-wdm"></a>RemoveLockMnRemove2 ルール (wdm)


**RemoveLockMnRemove2**ルールは、irp が転送される前に\_デバイスの要求\_削除するとき\_に、 [**IoAcquireRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)と[**IoReleaseRemoveLockAndWait**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelockandwait)の呼び出しが正しく使用されることを確認します。ドライバーを下げることができます。

このルールは、FDO および FIDO ドライバーにのみ適用されます。

たとえば、フィルタードライバー、FDO、および PDO で構成される PnP ドライバースタックを考えてみます。

PnP マネージャーは、スタックを通じて削除クエリを送信します。 システムの実行中は、FDO がアイドル状態になります。 FDO は、クエリの削除された状態の電源を切り、d0 IRP を要求します。 D0 IRP が到着する前に、PnP マネージャーは PnP の削除 IRP を送信し、その IRP はフィルタードライバーによって処理されます。 フィルタードライバーはスタックからデタッチし、その状態をクリーンアップします。 D0 はスタックの一番上に到達しますが、フィルタードライバーは、それを送信する場所を認識するためのコンテキストまたはデータがないため、スタックには送信しません。 FDO が、d0 IRP が到着するのを待機している間にハングしていますが、その IRP は停止しません。

**このエラーを回避するには**

1.  デバイスがデバイススタックからデタッチされる前に、 [**IoAcquireRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)は irp が次の種類の irp に対してスタックに転送される前に成功する必要があります。

    -   IRP\_\_クエリ\_削除
    -   IRP\_\_SUPRISE 削除
    -   IRP\_\_\_デバイスの削除

2.  [**IoDetachDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodetachdevice)または[**iodeletedevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodeletedevice)を呼び出す前に、 [**IoReleaseRemoveLockAndWait**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelockandwait)を呼び出す必要があります。 (これにより、すべての削除ロックがデバイスドライバーで確実に解放されます)。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>RemoveLockMnRemove2</strong>規則を指定します。</p>
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

[**IoAcquireRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)
[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)
[**IoReleaseRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock)
[**IoReleaseRemoveLockAndWait**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelockandwait)
[**pocalldriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)
 

 





