---
title: IrpPending の規則セット (WDM)
description: ドライバーをことを確認するこれらの規則を使用して正しく、アプリケーション I/O 要求パケット (IRP)。
ms.assetid: C4B5976B-7655-4FD1-B415-98C256873EBC
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: b9c2731d4d21fc5d3b83e8f4d5b32547cbfc87ef
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349909"
---
# <a name="irppending-rule-set-wdm"></a>IrpPending の規則セット (WDM)


ドライバーをことを確認するこれらの規則を使用して正しく、アプリケーション I/O 要求パケット (IRP)。

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
<td align="left"><p><a href="wdm-markdevicepower.md" data-raw-source="[&lt;strong&gt;MarkDevicePower&lt;/strong&gt;](wdm-markdevicepower.md)"> <strong>MarkDevicePower</strong> </a>ルールでは、S0 を SystemPowerState IRP の IRP_MN_SET_POWER に対し、IRP_MJ_POWER が保留を指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-markinginterlockedqueuedirps.md" data-raw-source="[&lt;strong&gt;MarkingInterlockedQueuedIrps&lt;/strong&gt;](wdm-markinginterlockedqueuedirps.md)"><strong>MarkingInterlockedQueuedIrps</strong></a></p></td>
<td align="left"><p><a href="wdm-markinginterlockedqueuedirps.md" data-raw-source="[&lt;strong&gt;MarkingInterlockedQueuedIrps&lt;/strong&gt;](wdm-markinginterlockedqueuedirps.md)"> <strong>MarkingInterlockedQueuedIrps</strong> </a>ルールでは、前に保留中、キューにそれをさらに処理するためのインタロックされた方法でと、ドライバーがその IRP を正しくマークことを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-markingqueuedirps.md" data-raw-source="[&lt;strong&gt;MarkingQueuedIrps&lt;/strong&gt;](wdm-markingqueuedirps.md)"><strong>MarkingQueuedIrps</strong></a></p></td>
<td align="left"><p><a href="wdm-markingqueuedirps.md" data-raw-source="[&lt;strong&gt;MarkingQueuedIrps&lt;/strong&gt;](wdm-markingqueuedirps.md)"> <strong>MarkingQueuedIrps</strong> </a>ルールでは、ドライバーを呼び出すことを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff549422" data-raw-source="[&lt;strong&gt;IoMarkIrpPending&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549422)"> <strong>IoMarkIrpPending</strong> </a>さらに処理が必要な IRP のスピン ロックを保持中にのみします。 このルールは、ドライバーがドライバー管理キューに IRP を追加するときにのみ適用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-markirppending.md" data-raw-source="[&lt;strong&gt;MarkIrpPending&lt;/strong&gt;](wdm-markirppending.md)"><strong>MarkIrpPending</strong></a></p></td>
<td align="left"><p><a href="wdm-markirppending.md" data-raw-source="[&lt;strong&gt;MarkIrpPending&lt;/strong&gt;](wdm-markirppending.md)"> <strong>MarkIrpPending</strong> </a>規則で指定されるたびに、ドライバーのディスパッチ ルーチンを呼び出すこと<a href="https://msdn.microsoft.com/library/windows/hardware/ff549422" data-raw-source="[&lt;strong&gt;IoMarkIrpPending&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549422)"> <strong>IoMarkIrpPending</strong></a>ドライバーを返しますディスパッチ ルーチンが終了したときにあります。 参照してください<a href="wdm-markirppending2.md" data-raw-source="[&lt;strong&gt;MarkIrpPending2&lt;/strong&gt;](wdm-markirppending2.md)"> <strong>MarkIrpPending2</strong> </a>の無償の仕様。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-markirppending2.md" data-raw-source="[&lt;strong&gt;MarkIrpPending2&lt;/strong&gt;](wdm-markirppending2.md)"><strong>MarkIrpPending2</strong></a></p></td>
<td align="left"><p><a href="wdm-markirppending2.md" data-raw-source="[&lt;strong&gt;MarkIrpPending2&lt;/strong&gt;](wdm-markirppending2.md)"> <strong>MarkIrpPending2</strong> </a>ディスパッチ ルーチンは STATUS_PENDING を返す場合に呼び出すことが規則の指定<a href="https://msdn.microsoft.com/library/windows/hardware/ff549422" data-raw-source="[&lt;strong&gt;IoMarkIrpPending&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549422)"> <strong>IoMarkIrpPending</strong> </a>またはIRP を下位のドライバーに渡されます。 参照してください<a href="wdm-markirppending.md" data-raw-source="[&lt;strong&gt;MarkIrpPending&lt;/strong&gt;](wdm-markirppending.md)"> <strong>MarkIrpPending</strong> </a>の無償の仕様。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-markpower.md" data-raw-source="[&lt;strong&gt;MarkPower&lt;/strong&gt;](wdm-markpower.md)"><strong>MarkPower</strong></a></p></td>
<td align="left"><p><a href="wdm-markpower.md" data-raw-source="[&lt;strong&gt;MarkPower&lt;/strong&gt;](wdm-markpower.md)"> <strong>MarkPower</strong> </a>ルールを指定する IRP_MN_SET_POWER に対し、IRP_MJ_POWER、 <strong>SystemPowerState</strong> S0 に IRP が保留。 このルールは、FDO および FIDO ドライバーのみに適用されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-markpowerdown.md" data-raw-source="[&lt;strong&gt;MarkPowerDown&lt;/strong&gt;](wdm-markpowerdown.md)"><strong>MarkPowerDown</strong></a></p></td>
<td align="left"><p><a href="wdm-markpowerdown.md" data-raw-source="[&lt;strong&gt;MarkPowerDown&lt;/strong&gt;](wdm-markpowerdown.md)"> <strong>MarkPowerDown</strong> </a>ルールを指定する IRP_MN_SET_POWER に対し、IRP_MJ_POWER、 <strong>SystemPowerState</strong> IRP s0 から [S1] に移動S5] は、保留します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-markqueryrelations.md" data-raw-source="[&lt;strong&gt;MarkQueryRelations&lt;/strong&gt;](wdm-markqueryrelations.md)"><strong>MarkQueryRelations</strong></a></p></td>
<td align="left"><p><a href="wdm-markqueryrelations.md" data-raw-source="[&lt;strong&gt;MarkQueryRelations&lt;/strong&gt;](wdm-markqueryrelations.md)"> <strong>MarkQueryRelations</strong> </a>ルールでは、ドライバーが保留 IRP_MN_QUERY_DEVICE_RELATIONS IRP をする必要がありますを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-markstartdevice.md" data-raw-source="[&lt;strong&gt;MarkStartDevice&lt;/strong&gt;](wdm-markstartdevice.md)"><strong>MarkStartDevice</strong></a></p></td>
<td align="left"><p><a href="wdm-markstartdevice.md" data-raw-source="[&lt;strong&gt;MarkStartDevice&lt;/strong&gt;](wdm-markstartdevice.md)"> <strong>MarkStartDevice</strong> </a>ルールを指定するドライバーのとれた IRP_MN_START_DEVICE IRP 正しくします。 このルールは、FDO および FIDO ドライバーのみに適用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-pendedcompletedrequest.md" data-raw-source="[&lt;strong&gt;PendedCompletedRequest&lt;/strong&gt;](wdm-pendedcompletedrequest.md)"><strong>PendedCompletedRequest</strong></a></p></td>
<td align="left"><p><a href="wdm-pendedcompletedrequest.md" data-raw-source="[&lt;strong&gt;PendedCompletedRequest&lt;/strong&gt;](wdm-pendedcompletedrequest.md)"> <strong>PendedCompletedRequest</strong> </a>ルールでは、ドライバーのディスパッチ ルーチンを返さないこと STATUS_PENDING IRP のドライバーが呼び出された場合を指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff548343" data-raw-source="[&lt;strong&gt;IoCompleteRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548343)"> <strong>IoCompleteRequest</strong> </a>の IRP を受信します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-pendedcompletedrequest2.md" data-raw-source="[&lt;strong&gt;PendedCompletedRequest2&lt;/strong&gt;](wdm-pendedcompletedrequest2.md)"><strong>PendedCompletedRequest2</strong></a></p></td>
<td align="left"><p><a href="wdm-pendedcompletedrequest2.md" data-raw-source="[&lt;strong&gt;PendedCompletedRequest2&lt;/strong&gt;](wdm-pendedcompletedrequest2.md)"> <strong>PendedCompletedRequest2</strong> </a>ルールの呼び出しの後に待機が必要なことを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff548336" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548336)"><strong>保留</strong></a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff559654" data-raw-source="[&lt;strong&gt;PoCallDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559654)"><strong>PoCallDriver</strong> </a>ディスパッチ ルーチンは保留中の IRP を済ませるためです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-pendedcompletedrequest3.md" data-raw-source="[&lt;strong&gt;PendedCompletedRequest3&lt;/strong&gt;](wdm-pendedcompletedrequest3.md)"><strong>PendedCompletedRequest3</strong></a></p></td>
<td align="left"><p><a href="wdm-pendedcompletedrequest3.md" data-raw-source="[&lt;strong&gt;PendedCompletedRequest3&lt;/strong&gt;](wdm-pendedcompletedrequest3.md)"> <strong>PendedCompletedRequest3</strong> </a>ルールでは、保留中の IRP がへの呼び出しで完了しない必要がありますを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff548343" data-raw-source="[&lt;strong&gt;IoCompleteRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548343)"> <strong>IoCompleteRequest</strong></a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-pendedcompletedrequestex.md" data-raw-source="[&lt;strong&gt;PendedCompletedRequestEx&lt;/strong&gt;](wdm-pendedcompletedrequestex.md)"><strong>PendedCompletedRequestEx</strong></a></p></td>
<td align="left"><p><a href="wdm-pendedcompletedrequestex.md" data-raw-source="[&lt;strong&gt;PendedCompletedRequestEx&lt;/strong&gt;](wdm-pendedcompletedrequestex.md)"> <strong>PendedCompletedRequestEx</strong> </a>ルールでは、ドライバーを呼び出さないことを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff548343" data-raw-source="[&lt;strong&gt;IoCompleteRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548343)"> <strong>IoCompleteRequest</strong> </a>保留中の IRP の。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-startdevicewait.md" data-raw-source="[&lt;strong&gt;StartDeviceWait&lt;/strong&gt;](wdm-startdevicewait.md)"><strong>StartDeviceWait</strong></a></p></td>
<td align="left"><p><a href="wdm-startdevicewait.md" data-raw-source="[&lt;strong&gt;StartDeviceWait&lt;/strong&gt;](wdm-startdevicewait.md)"> <strong>StartDeviceWait</strong> </a>ルールでは、ドライバーを呼び出さないことを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff553350" data-raw-source="[&lt;strong&gt;KeWaitForSingleObject&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553350)"> <strong>kewaitforsingleobject の 1</strong> </a>デバイスの起動のコンテキストでIRP します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-startdevicewait2.md" data-raw-source="[&lt;strong&gt;StartDeviceWait2&lt;/strong&gt;](wdm-startdevicewait2.md)"><strong>StartDeviceWait2</strong></a></p></td>
<td align="left"><p><a href="wdm-startdevicewait2.md" data-raw-source="[&lt;strong&gt;StartDeviceWait2&lt;/strong&gt;](wdm-startdevicewait2.md)"> <strong>StartDeviceWait2</strong> </a>ルールでは、ドライバーを呼び出さないことを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff553350" data-raw-source="[&lt;strong&gt;KeWaitForSingleObject&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553350)"> <strong>kewaitforsingleobject の 1</strong> </a>デバイスの起動のコンテキストでIRP します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-startdevicewait3.md" data-raw-source="[&lt;strong&gt;StartDeviceWait3&lt;/strong&gt;](wdm-startdevicewait3.md)"><strong>StartDeviceWait3</strong></a></p></td>
<td align="left"><p><a href="wdm-startdevicewait3.md" data-raw-source="[&lt;strong&gt;StartDeviceWait3&lt;/strong&gt;](wdm-startdevicewait3.md)"> <strong>StartDeviceWait3</strong> </a>ルールでは、ドライバーを呼び出さないことを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff553350" data-raw-source="[&lt;strong&gt;KeWaitForSingleObject&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553350)"> <strong>kewaitforsingleobject の 1</strong> </a>デバイスの起動のコンテキストでIRP します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-startdevicewait4.md" data-raw-source="[&lt;strong&gt;StartDeviceWait4&lt;/strong&gt;](wdm-startdevicewait4.md)"><strong>StartDeviceWait4</strong></a></p></td>
<td align="left"><p><a href="wdm-startdevicewait4.md" data-raw-source="[&lt;strong&gt;StartDeviceWait4&lt;/strong&gt;](wdm-startdevicewait4.md)"> <strong>StartDeviceWait4</strong> </a>ルールでは、ドライバーを呼び出さないことを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff553350" data-raw-source="[&lt;strong&gt;KeWaitForSingleObject&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553350)"> <strong>kewaitforsingleobject の 1</strong> </a>デバイスの起動のコンテキストでIRP します。</p></td>
</tr>
</tbody>
</table>

 

**IrpPending ルールを選択するには、次のように設定します。**

1.  Microsoft Visual Studio で、ドライバーのプロジェクト (.vcxProj) を選択します。 **ドライバー**  メニューのをクリックして**Static Driver Verifier を起動しています**.

2.  をクリックして、**ルール**タブ。**規則セット**、 **IrpPending**します。

    Visual Studio の開発者コマンド プロンプト ウィンドウから既定のルールを選択するには、次のように指定します。 **IrpPending.sdv**で、 **/check**オプション。 以下に例を示します。

    ```
    msbuild /t:sdv /p:Inputs="/check:IrpPending.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    詳細については、[ドライバーで障害を検出する Static Driver Verifier を使用して](https://msdn.microsoft.com/library/windows/hardware/hh454281)と[Static Driver Verifier のコマンド (MSBuild)](https://msdn.microsoft.com/library/windows/hardware/hh466459)を参照してください。

 

 





