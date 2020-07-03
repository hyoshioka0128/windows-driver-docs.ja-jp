---
title: RemoveLockQueryMnRemove ルール (wdm)
description: RemoveLockQueryMnRemove ルールは、 \_ \_ MinorFunction irp クエリでデバイスを削除するときに、IoAcquireRemoveLock と IoReleaseRemoveLock の呼び出しが正しく使用されていることを確認し \_ \_ \_ \_ ます。
ms.assetid: 593B8305-EA61-4857-9304-A8319A8E0017
ms.date: 05/21/2018
keywords:
- RemoveLockQueryMnRemove ルール (wdm)
topic_type:
- apiref
api_name:
- RemoveLockQueryMnRemove
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f8452c1ca8630daf18592fcdb880a36e3941c010
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916160"
---
# <a name="removelockquerymnremove-rule-wdm"></a>RemoveLockQueryMnRemove ルール (wdm)


**RemoveLockQueryMnRemove**ルールは、 [**IoAcquireRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock) [**IoReleaseRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock) \_ \_ minorfunction irp クエリでデバイスを削除するときに、IoAcquireRemoveLock と IoReleaseRemoveLock の呼び出しが正しく使用されていることを確認し \_ \_ \_ \_ ます。 ドライバーは、IRP をスタックに転送する前に、削除ロックを取得する必要があります。

このルールは、FDO および FIDO ドライバーにのみ適用されます。

たとえば、フィルタードライバー、FDO、および PDO で構成される PnP ドライバースタックを考えてみます。

PnP マネージャーは、スタックを通じて削除クエリを送信します。 システムの実行中は、FDO がアイドル状態になります。 FDO は、クエリの削除された状態の電源を切り、d0 IRP を要求します。 D0 IRP が到着する前に、PnP マネージャーは PnP の削除 IRP を送信し、その IRP はフィルタードライバーによって処理されます。 フィルタードライバーはスタックからデタッチし、その状態をクリーンアップします。 D0 はスタックの一番上に到達しますが、フィルタードライバーは、それを送信する場所を認識するためのコンテキストまたはデータがないため、スタックには送信しません。 FDO が、d0 IRP が到着するのを待機している間にハングしていますが、その IRP は停止しません。

**このエラーを回避するには**

1.  デバイスがデバイススタックからデタッチされる前に、 [**IoAcquireRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)は irp が次の種類の irp に対してスタックに転送される前に成功する必要があります。

    -   IRP を実行する \_ \_ クエリの \_ 削除
    -   IRP \_ の \_ \_ 消去
    -   IRP のすべての \_ \_ デバイスの削除 \_

2.  [**IoDetachDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodetachdevice)または[**iodeletedevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodeletedevice)を呼び出す前に、 [**IoReleaseRemoveLockAndWait**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelockandwait)を呼び出す必要があります。 (これにより、すべての削除ロックがデバイスドライバーで確実に解放されます)。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>RemoveLockQueryMnRemove</strong>規則を指定します。</p>
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

[**IoAcquireRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock) 
[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) 
[**IoReleaseRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock) 
[**Pocalldriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)
 

 





