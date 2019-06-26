---
title: RemoveLockQueryMnRemove ルール (wdm)
description: IRP の処理時に IoAcquireRemoveLock および IoReleaseRemoveLock への呼び出しが正しく使用 RemoveLockQueryMnRemove ルールを確認します\_MJ\_MinorFunction IRP の PNP\_MN\_クエリ\_削除\_デバイス。
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
ms.openlocfilehash: 7963c30cd3cc1343641c812c294b796a76b5fb89
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393576"
---
# <a name="removelockquerymnremove-rule-wdm"></a>RemoveLockQueryMnRemove ルール (wdm)


**RemoveLockQueryMnRemove**への呼び出し規則を確認します[ **IoAcquireRemoveLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioacquireremovelock)と[ **IoReleaseRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioreleaseremovelock)が IRP の処理時に正しく使用\_MJ\_MinorFunction IRP の PNP\_MN\_クエリ\_削除\_デバイス。 ドライバーは IRP が下位のスタックを転送する前に削除ロックを取得する必要があります。

このルールは、FDO および FIDO ドライバーのみに適用されます。

たとえば、フィルター ドライバーの FDO と PDO で構成される PnP ドライバー スタックがあるとします。

PnP マネージャーでは、クエリの削除がスタックを送信します。 アイドル状態のシステムの実行中に、FDO になっています。 FDO 決定電源ダウン削除クエリの状態で d0 IRP を要求します。 D0 IRP が到着すると、前に、PnP マネージャーは、PnP IRP を削除して、フィルター ドライバーが IRP が処理されたことを送信します。 フィルター ドライバーでは、スタックからデタッチされ、その状態をクリーンアップします。 スタックの上部にある、d0 が到着しますが、フィルター ドライバーは送信しません下位のスタックが存在しないコンテキストまたはデータがもはや送信先を判断します。 FDO は d0 IRP IRP がないことが到着するを待つハング状態にします。

**このエラーを回避する**

1.  デバイスは、デバイス スタックからデタッチされる前に[ **IoAcquireRemoveLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioacquireremovelock) IRP の次の種類のスタックを IRP が転送される前に、成功する必要があります。

    -   IRP\_MN\_クエリ\_削除
    -   IRP\_MN\_SUPRISE\_REMOVAL
    -   IRP\_MN\_削除\_デバイス

2.  [**IoReleaseRemoveLockAndWait** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioreleaseremovelockandwait)呼び出す前に呼び出す必要がある[ **IoDetachDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iodetachdevice)または[ **IoDeleteDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iodeletedevice). (これにより、デバイス ドライバーのすべての削除ロックが解放される)。

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
<td align="left"><p>実行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>を指定し、 <strong>RemoveLockQueryMnRemove</strong>ルール。</p>
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
[**IoReleaseRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioreleaseremovelock) 
 [ **PoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver)
 

 





