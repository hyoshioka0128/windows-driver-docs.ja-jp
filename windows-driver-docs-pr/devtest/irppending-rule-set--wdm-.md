---
title: IrpPending の規則セット (WDM)
description: これらのルールを使用して、ドライバーが i/o 要求パケット (IRP) を正しく pends していることを確認します。
ms.assetid: C4B5976B-7655-4FD1-B415-98C256873EBC
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0895debb772d4f8e2ebd4afcfe237e5a981445d9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840257"
---
# <a name="irppending-rule-set-wdm"></a>IrpPending の規則セット (WDM)


これらのルールを使用して、ドライバーが i/o 要求パケット (IRP) を正しく pends していることを確認します。

## <a name="in-this-section"></a>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">トピック</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="wdm-markdevicepower.md" data-raw-source="[&lt;strong&gt;MarkDevicePower&lt;/strong&gt;](wdm-markdevicepower.md)"><strong>MarkDevicePower</strong></a></p></td>
<td align="left"><p><a href="wdm-markdevicepower.md" data-raw-source="[&lt;strong&gt;MarkDevicePower&lt;/strong&gt;](wdm-markdevicepower.md)"><strong>Markdevicepower</strong></a>ルールでは、IRP_MN_SET_POWER FOR SystemPowerState IRP を IRP_MJ_POWER とすることを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-markinginterlockedqueuedirps.md" data-raw-source="[&lt;strong&gt;MarkingInterlockedQueuedIrps&lt;/strong&gt;](wdm-markinginterlockedqueuedirps.md)"><strong>MarkingInterlockedQueuedIrps</strong></a></p></td>
<td align="left"><p><a href="wdm-markinginterlockedqueuedirps.md" data-raw-source="[&lt;strong&gt;MarkingInterlockedQueuedIrps&lt;/strong&gt;](wdm-markinginterlockedqueuedirps.md)"><strong>MarkingInterlockedQueuedIrps</strong></a>規則は、後続の処理のためにインタロックされた形式で IRP をキューに登録する前に、ドライバーが IRP を保留中としてマークするように指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-markingqueuedirps.md" data-raw-source="[&lt;strong&gt;MarkingQueuedIrps&lt;/strong&gt;](wdm-markingqueuedirps.md)"><strong>MarkingQueuedIrps</strong></a></p></td>
<td align="left"><p><a href="wdm-markingqueuedirps.md" data-raw-source="[&lt;strong&gt;MarkingQueuedIrps&lt;/strong&gt;](wdm-markingqueuedirps.md)"><strong>Markingqueuedirps</strong></a>ルールでは、スピンロックを保持しているときにのみさらに処理する必要がある IRP に対して、ドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending" data-raw-source="[&lt;strong&gt;IoMarkIrpPending&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)"><strong>Iomarkirppending</strong></a>を呼び出すことを指定します。 この規則は、ドライバーによって管理されるキューに IRP を追加する場合にのみ適用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-markirppending.md" data-raw-source="[&lt;strong&gt;MarkIrpPending&lt;/strong&gt;](wdm-markirppending.md)"><strong>MarkIrpPending</strong></a></p></td>
<td align="left"><p><a href="wdm-markirppending.md" data-raw-source="[&lt;strong&gt;MarkIrpPending&lt;/strong&gt;](wdm-markirppending.md)"><strong>Markirppending</strong></a>ルールは、ドライバーディスパッチルーチンが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending" data-raw-source="[&lt;strong&gt;IoMarkIrpPending&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)"><strong>Iomarkirppending</strong></a>を呼び出すたびに、ディスパッチルーチンが終了したときに、ドライバーがありますを返すことを指定します。 無料の仕様については、「 <a href="wdm-markirppending2.md" data-raw-source="[&lt;strong&gt;MarkIrpPending2&lt;/strong&gt;](wdm-markirppending2.md)"><strong>MarkIrpPending2</strong></a> 」を参照してください。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-markirppending2.md" data-raw-source="[&lt;strong&gt;MarkIrpPending2&lt;/strong&gt;](wdm-markirppending2.md)"><strong>MarkIrpPending2</strong></a></p></td>
<td align="left"><p><a href="wdm-markirppending2.md" data-raw-source="[&lt;strong&gt;MarkIrpPending2&lt;/strong&gt;](wdm-markirppending2.md)"><strong>MarkIrpPending2</strong></a>ルールは、ディスパッチルーチンがありますを返す場合に、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending" data-raw-source="[&lt;strong&gt;IoMarkIrpPending&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)"><strong>Iomarkirppending</strong></a>を呼び出したか、または IRP を下位ドライバーに渡したことを指定します。 無料仕様については、「 <a href="wdm-markirppending.md" data-raw-source="[&lt;strong&gt;MarkIrpPending&lt;/strong&gt;](wdm-markirppending.md)"><strong>Markirppending</strong></a> 」を参照してください。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-markpower.md" data-raw-source="[&lt;strong&gt;MarkPower&lt;/strong&gt;](wdm-markpower.md)"><strong>MarkPower</strong></a></p></td>
<td align="left"><p><a href="wdm-markpower.md" data-raw-source="[&lt;strong&gt;MarkPower&lt;/strong&gt;](wdm-markpower.md)"><strong>Markpower</strong></a> rule は、IRP_MN_SET_POWER for <strong>SystemPowerState</strong> IRP が S0 に IRP_MJ_POWER することを指定します。 このルールは、FDO および FIDO ドライバーにのみ適用されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-markpowerdown.md" data-raw-source="[&lt;strong&gt;MarkPowerDown&lt;/strong&gt;](wdm-markpowerdown.md)"><strong>MarkPowerDown</strong></a></p></td>
<td align="left"><p><a href="wdm-markpowerdown.md" data-raw-source="[&lt;strong&gt;MarkPowerDown&lt;/strong&gt;](wdm-markpowerdown.md)"><strong>MarkPowerDown</strong></a>規則は、 <strong>SYSTEMPOWERSTATE</strong> IRP の IRP_MJ_POWER が s0 から [S1...S5] は保留されています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-markqueryrelations.md" data-raw-source="[&lt;strong&gt;MarkQueryRelations&lt;/strong&gt;](wdm-markqueryrelations.md)"><strong>MarkQueryRelations</strong></a></p></td>
<td align="left"><p><a href="wdm-markqueryrelations.md" data-raw-source="[&lt;strong&gt;MarkQueryRelations&lt;/strong&gt;](wdm-markqueryrelations.md)"><strong>Markqueryrelations</strong></a>ルールでは、ドライバーが IRP_MN_QUERY_DEVICE_RELATIONS IRP を保留する必要があることを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-markstartdevice.md" data-raw-source="[&lt;strong&gt;MarkStartDevice&lt;/strong&gt;](wdm-markstartdevice.md)"><strong>MarkStartDevice</strong></a></p></td>
<td align="left"><p><a href="wdm-markstartdevice.md" data-raw-source="[&lt;strong&gt;MarkStartDevice&lt;/strong&gt;](wdm-markstartdevice.md)"><strong>Markstartdevice</strong></a>ルールは、ドライバーが IRP_MN_START_DEVICE IRP を正しく pends ことを指定します。 このルールは、FDO および FIDO ドライバーにのみ適用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-pendedcompletedrequest.md" data-raw-source="[&lt;strong&gt;PendedCompletedRequest&lt;/strong&gt;](wdm-pendedcompletedrequest.md)"><strong>PendedCompletedRequest</strong></a></p></td>
<td align="left"><p><a href="wdm-pendedcompletedrequest.md" data-raw-source="[&lt;strong&gt;PendedCompletedRequest&lt;/strong&gt;](wdm-pendedcompletedrequest.md)"><strong>PendedCompletedRequest</strong></a>ルールは、ドライバーが受信 Irp で<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest" data-raw-source="[&lt;strong&gt;IoCompleteRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)"><strong>IoCompleteRequest</strong></a>を呼び出した場合に、ドライバーのディスパッチルーチンが irp でありますを返さないことを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-pendedcompletedrequest2.md" data-raw-source="[&lt;strong&gt;PendedCompletedRequest2&lt;/strong&gt;](wdm-pendedcompletedrequest2.md)"><strong>PendedCompletedRequest2</strong></a></p></td>
<td align="left"><p><a href="wdm-pendedcompletedrequest2.md" data-raw-source="[&lt;strong&gt;PendedCompletedRequest2&lt;/strong&gt;](wdm-pendedcompletedrequest2.md)"><strong>PendedCompletedRequest2</strong></a>規則は、ディスパッチルーチンが保留中の IRP を完了できるため、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)"><strong>IoCallDriver</strong></a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver" data-raw-source="[&lt;strong&gt;PoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)"><strong>pocalldriver</strong></a>を呼び出した後に待機が必要であることを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-pendedcompletedrequest3.md" data-raw-source="[&lt;strong&gt;PendedCompletedRequest3&lt;/strong&gt;](wdm-pendedcompletedrequest3.md)"><strong>PendedCompletedRequest3</strong></a></p></td>
<td align="left"><p><a href="wdm-pendedcompletedrequest3.md" data-raw-source="[&lt;strong&gt;PendedCompletedRequest3&lt;/strong&gt;](wdm-pendedcompletedrequest3.md)"><strong>PendedCompletedRequest3</strong></a>規則は、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest" data-raw-source="[&lt;strong&gt;IoCompleteRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)"><strong>IoCompleteRequest</strong></a>の呼び出しで保留中の IRP を完了しないように指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-pendedcompletedrequestex.md" data-raw-source="[&lt;strong&gt;PendedCompletedRequestEx&lt;/strong&gt;](wdm-pendedcompletedrequestex.md)"><strong>PendedCompletedRequestEx</strong></a></p></td>
<td align="left"><p><a href="wdm-pendedcompletedrequestex.md" data-raw-source="[&lt;strong&gt;PendedCompletedRequestEx&lt;/strong&gt;](wdm-pendedcompletedrequestex.md)"><strong>PendedCompletedRequestEx</strong></a>規則は、ドライバーが保留中の IRP の<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest" data-raw-source="[&lt;strong&gt;IoCompleteRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)"><strong>IoCompleteRequest</strong></a>を呼び出さないことを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-startdevicewait.md" data-raw-source="[&lt;strong&gt;StartDeviceWait&lt;/strong&gt;](wdm-startdevicewait.md)"><strong>StartDeviceWait</strong></a></p></td>
<td align="left"><p><a href="wdm-startdevicewait.md" data-raw-source="[&lt;strong&gt;StartDeviceWait&lt;/strong&gt;](wdm-startdevicewait.md)"><strong>Startdevicewait</strong></a>ルールでは、ドライバーが START device IRP のコンテキストで<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject" data-raw-source="[&lt;strong&gt;KeWaitForSingleObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject)"><strong>KeWaitForSingleObject</strong></a>を呼び出さないように指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-startdevicewait2.md" data-raw-source="[&lt;strong&gt;StartDeviceWait2&lt;/strong&gt;](wdm-startdevicewait2.md)"><strong>StartDeviceWait2</strong></a></p></td>
<td align="left"><p><a href="wdm-startdevicewait2.md" data-raw-source="[&lt;strong&gt;StartDeviceWait2&lt;/strong&gt;](wdm-startdevicewait2.md)"><strong>StartDeviceWait2</strong></a>規則は、ドライバーが START device IRP のコンテキストで<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject" data-raw-source="[&lt;strong&gt;KeWaitForSingleObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject)"><strong>KeWaitForSingleObject</strong></a>を呼び出さないように指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-startdevicewait3.md" data-raw-source="[&lt;strong&gt;StartDeviceWait3&lt;/strong&gt;](wdm-startdevicewait3.md)"><strong>StartDeviceWait3</strong></a></p></td>
<td align="left"><p><a href="wdm-startdevicewait3.md" data-raw-source="[&lt;strong&gt;StartDeviceWait3&lt;/strong&gt;](wdm-startdevicewait3.md)"><strong>StartDeviceWait3</strong></a>規則は、ドライバーが START device IRP のコンテキストで<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject" data-raw-source="[&lt;strong&gt;KeWaitForSingleObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject)"><strong>KeWaitForSingleObject</strong></a>を呼び出さないように指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-startdevicewait4.md" data-raw-source="[&lt;strong&gt;StartDeviceWait4&lt;/strong&gt;](wdm-startdevicewait4.md)"><strong>StartDeviceWait4</strong></a></p></td>
<td align="left"><p><a href="wdm-startdevicewait4.md" data-raw-source="[&lt;strong&gt;StartDeviceWait4&lt;/strong&gt;](wdm-startdevicewait4.md)"><strong>StartDeviceWait4</strong></a>規則は、ドライバーが START device IRP のコンテキストで<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject" data-raw-source="[&lt;strong&gt;KeWaitForSingleObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject)"><strong>KeWaitForSingleObject</strong></a>を呼び出さないように指定します。</p></td>
</tr>
</tbody>
</table>

 

**IrpPending 規則セットを選択するには**

1.  Microsoft Visual Studio でドライバープロジェクト (.Vcxproj) を選択します。 **[ドライバー]** メニューの **[静的ドライバー検証ツールの起動]** をクリックします。

2.  **[ルール]** タブをクリックします。 **[ルールセット]** で **[irppending]** を選択します。

    Visual Studio 開発者コマンドプロンプトウィンドウから既定の規則セットを選択するには、 **/チェック**オプションを使用して、 **irppending**を指定します。 次に、例を示します。

    ```
    msbuild /t:sdv /p:Inputs="/check:IrpPending.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    詳細については、「 [Using Static Driver verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers) 」を参照して、ドライバーと[静的ドライバー検証コマンド (MSBuild)](https://docs.microsoft.com/windows-hardware/drivers/devtest/-static-driver-verifier-commands--msbuild-)で欠陥を検出してください。

 

 





