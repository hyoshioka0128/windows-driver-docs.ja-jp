---
title: 警告の規則セット (WDM)
description: これらの規則を使用すると、さまざまなコンテキストでは、ドライバーが Irp を正しく処理を次のように Microsoft が推奨されるベスト プラクティスを確認します。
ms.assetid: 29374BBE-D1DF-48C0-80A9-96CBAC6D8A22
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 989a17b7030a24cdca3611bb25ed600d3ab8e441
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67394014"
---
# <a name="warning-rule-set-wdm"></a>警告の規則セット (WDM)


これらの規則を使用すると、さまざまなコンテキストでは、ドライバーが Irp を正しく処理を次のように Microsoft が推奨されるベスト プラクティスを確認します。

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
<td align="left"><p><a href="wdm-checkdeviceobjectflags.md" data-raw-source="[&lt;strong&gt;CheckDeviceObjectFlags&lt;/strong&gt;](wdm-checkdeviceobjectflags.md)"><strong>CheckDeviceObjectFlags</strong></a></p></td>
<td align="left"><p><a href="wdm-checkdeviceobjectflags.md" data-raw-source="[&lt;strong&gt;CheckDeviceObjectFlags&lt;/strong&gt;](wdm-checkdeviceobjectflags.md)"> <strong>CheckDeviceObjectFlags</strong> </a>ルールでは、バス ドライバーが、FDO と子 Pdo DO_POWER_PAGABLE と DO_POWER_INRUSH デバイス オブジェクトのフラグが一貫して設定されているを確認する必要がありますように指定します。 このルールは、バス ドライバーのみに適用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-completioneventchecking.md" data-raw-source="[&lt;strong&gt;CompletionEventChecking&lt;/strong&gt;](wdm-completioneventchecking.md)"><strong>CompletionEventChecking</strong></a></p></td>
<td align="left"><p><a href="wdm-completioneventchecking.md" data-raw-source="[&lt;strong&gt;CompletionEventChecking&lt;/strong&gt;](wdm-completioneventchecking.md)"> <strong>CompletionEventChecking</strong> </a>ルールでは、ドライバーは呼び出さないことを指定します<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iomarkirppending" data-raw-source="[&lt;strong&gt;IoMarkIrpPending&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iomarkirppending)"> <strong>IoMarkIrpPending</strong> </a>と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesetevent" data-raw-source="[&lt;strong&gt;KeSetEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesetevent)"> <strong>KeSetEvent</strong> </a>同じ IRP の完了のルーチンでします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-deletedevice.md" data-raw-source="[&lt;strong&gt;DeleteDevice&lt;/strong&gt;](wdm-deletedevice.md)"><strong>DeleteDevice</strong></a></p></td>
<td align="left"><p><a href="wdm-deletedevice.md" data-raw-source="[&lt;strong&gt;DeleteDevice&lt;/strong&gt;](wdm-deletedevice.md)"> <strong>DeleteDevice</strong> </a>ルールは、ドライバーが呼び出しの後に、デバイス オブジェクトを維持するには、I/O マネージャーまたは PnP マネージャーに依存する必要がありますを指定します<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iodeletedevice" data-raw-source="[&lt;strong&gt;IoDeleteDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iodeletedevice)"> <strong>IoDeleteDevice</strong></a>.</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-multremovelock.md" data-raw-source="[&lt;strong&gt;MultRemoveLock&lt;/strong&gt;](wdm-multremovelock.md)"><strong>MultRemoveLock</strong></a></p></td>
<td align="left"><p><a href="wdm-multremovelock.md" data-raw-source="[&lt;strong&gt;MultRemoveLock&lt;/strong&gt;](wdm-multremovelock.md)"> <strong>MultRemoveLock</strong> </a>ことを確認しますルール<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioacquireremovelock" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioacquireremovelock)"> <strong>IoAcquireRemoveLock</strong> </a>は一意の削除ロックを 1 つだけで呼び出されます。 これは、警告ルールです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-pagedcode.md" data-raw-source="[&lt;strong&gt;PagedCode&lt;/strong&gt;](wdm-pagedcode.md)"><strong>PagedCode</strong></a></p></td>
<td align="left"><p><a href="wdm-pagedcode.md" data-raw-source="[&lt;strong&gt;PagedCode&lt;/strong&gt;](wdm-pagedcode.md)"> <strong>PagedCode</strong> </a>ルールでは、ドライバーを呼び出すことを指定します、 <a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer" data-raw-source="[&lt;strong&gt;PAGED_CODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)"> <strong>PAGED_CODE</strong> </a>マクロで実行されている場合にのみ<strong>IRQL &lt;= APC_LEVEL</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-pagedcodeatpowertrans.md" data-raw-source="[&lt;strong&gt;PagedCodeAtPowerTrans&lt;/strong&gt;](wdm-pagedcodeatpowertrans.md)"><strong>PagedCodeAtPowerTrans</strong></a></p></td>
<td align="left"><p><a href="wdm-pagedcodeatpowertrans.md" data-raw-source="[&lt;strong&gt;PagedCodeAtPowerTrans&lt;/strong&gt;](wdm-pagedcodeatpowertrans.md)"> <strong>PagedCodeAtPowerTrans</strong> </a>ルールでは、ドライバーを呼び出さないことを指定します<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer" data-raw-source="[&lt;strong&gt;PAGED_CODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)"> <strong>PAGED_CODE</strong> </a> IRP_MJ_ システムへの応答中には電源 Irp (IRP_MN_SET_POWER) と、デバイスに対し、IRP_MJ_POWER Irp (IRP_MN_SET_POWER) にします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-reservedddis.md" data-raw-source="[&lt;strong&gt;ReservedDDIs&lt;/strong&gt;](wdm-reservedddis.md)"><strong>ReservedDDIs</strong></a></p></td>
<td align="left"><p><a href="wdm-reservedddis.md" data-raw-source="[&lt;strong&gt;ReservedDDIs&lt;/strong&gt;](wdm-reservedddis.md)"> <strong>ReservedDDIs</strong> </a>ルールは、ドライバーは、予約済みの関数を呼び出さないことを確認します。</p></td>
</tr>
</tbody>
</table>

 

**警告ルールを選択するには、次のように設定します。**

1.  Microsoft Visual Studio で、ドライバーのプロジェクト (.vcxProj) を選択します。 **ドライバー**  メニューのをクリックして**Static Driver Verifier を起動しています**.

2.  をクリックして、**ルール**タブ。**規則セット**、**警告**します。

    Visual Studio の開発者コマンド プロンプト ウィンドウから既定のルールを選択するには、次のように指定します。 **Warning.sdv**で、 **/check**オプション。 次に、例を示します。

    ```
    msbuild /t:sdv /p:Inputs="/check:Warning.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    詳細については、次を参照してください。[ドライバーで障害を検出する Static Driver Verifier を使用して](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)と[Static Driver Verifier のコマンド (MSBuild)](https://docs.microsoft.com/windows-hardware/drivers/devtest/-static-driver-verifier-commands--msbuild-)します。

 

 





