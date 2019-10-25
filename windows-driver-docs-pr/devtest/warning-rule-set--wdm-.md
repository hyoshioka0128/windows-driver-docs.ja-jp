---
title: 警告の規則セット (WDM)
description: これらのルールを使用して、ドライバーがさまざまなコンテキストで Irp を正しく処理できること、および Microsoft の推奨されるベストプラクティスに従うことを確認します。
ms.assetid: 29374BBE-D1DF-48C0-80A9-96CBAC6D8A22
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: b54e23f7b66313cf78989336f2cfa1162535b006
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839984"
---
# <a name="warning-rule-set-wdm"></a>警告の規則セット (WDM)


これらのルールを使用して、ドライバーがさまざまなコンテキストで Irp を正しく処理できること、および Microsoft の推奨されるベストプラクティスに従うことを確認します。

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
<td align="left"><p><a href="wdm-checkdeviceobjectflags.md" data-raw-source="[&lt;strong&gt;CheckDeviceObjectFlags&lt;/strong&gt;](wdm-checkdeviceobjectflags.md)"><strong>Checkdeviceobjectflags</strong></a>規則は、DO_POWER_PAGABLE と DO_POWER_INRUSH のデバイスオブジェクトフラグが FDO と子 pdos に対して一貫して設定されていることをバスドライバーが確認する必要があることを指定します。 このルールは、バスドライバーにのみ適用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-completioneventchecking.md" data-raw-source="[&lt;strong&gt;CompletionEventChecking&lt;/strong&gt;](wdm-completioneventchecking.md)"><strong>補完 Eventチェック</strong></a></p></td>
<td align="left"><p>Completion <a href="wdm-completioneventchecking.md" data-raw-source="[&lt;strong&gt;CompletionEventChecking&lt;/strong&gt;](wdm-completioneventchecking.md)"><strong>Event検査</strong></a>規則は、同じ IRP の完了ルーチンで、ドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending" data-raw-source="[&lt;strong&gt;IoMarkIrpPending&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)"><strong>Iomarkirppending</strong></a>と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent" data-raw-source="[&lt;strong&gt;KeSetEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent)"><strong>KeSetEvent</strong></a>を呼び出さないことを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-deletedevice.md" data-raw-source="[&lt;strong&gt;DeleteDevice&lt;/strong&gt;](wdm-deletedevice.md)"><strong>DeleteDevice</strong></a></p></td>
<td align="left"><p><a href="wdm-deletedevice.md" data-raw-source="[&lt;strong&gt;DeleteDevice&lt;/strong&gt;](wdm-deletedevice.md)"><strong>Deletedevice</strong></a>ルールは、ドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodeletedevice" data-raw-source="[&lt;strong&gt;IoDeleteDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodeletedevice)"><strong>iodeletedevice</strong></a>の呼び出し後に DeviceObject alive を維持するために、I/o マネージャーまたは PnP マネージャーに依存しないように指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-multremovelock.md" data-raw-source="[&lt;strong&gt;MultRemoveLock&lt;/strong&gt;](wdm-multremovelock.md)"><strong>MultRemoveLock</strong></a></p></td>
<td align="left"><p><a href="wdm-multremovelock.md" data-raw-source="[&lt;strong&gt;MultRemoveLock&lt;/strong&gt;](wdm-multremovelock.md)"><strong>MultRemoveLock</strong></a>ルールは、一意の削除ロックを1つだけ使用して<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)"><strong>IoAcquireRemoveLock</strong></a>が呼び出されることを確認します。 これは警告ルールです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-pagedcode.md" data-raw-source="[&lt;strong&gt;PagedCode&lt;/strong&gt;](wdm-pagedcode.md)"><strong>PagedCode</strong></a></p></td>
<td align="left"><p><a href="wdm-pagedcode.md" data-raw-source="[&lt;strong&gt;PagedCode&lt;/strong&gt;](wdm-pagedcode.md)"><strong>PagedCode</strong></a>規則は、 <strong>IRQL &lt;= APC_LEVEL</strong>で実行されている場合にのみ、ドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer" data-raw-source="[&lt;strong&gt;PAGED_CODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)"><strong>PAGED_CODE</strong></a>マクロを呼び出すように指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-pagedcodeatpowertrans.md" data-raw-source="[&lt;strong&gt;PagedCodeAtPowerTrans&lt;/strong&gt;](wdm-pagedcodeatpowertrans.md)"><strong>PagedCodeAtPowerTrans</strong></a></p></td>
<td align="left"><p><a href="wdm-pagedcodeatpowertrans.md" data-raw-source="[&lt;strong&gt;PagedCodeAtPowerTrans&lt;/strong&gt;](wdm-pagedcodeatpowertrans.md)"><strong>PagedCodeAtPowerTrans</strong></a>規則は、システム IRP_MJ_POWER IRP (IRP_MN_SET_POWER) およびデバイス IRP_MJ_POWER IRP (IRP_MN_SET_POWER) に応答しているときに、ドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer" data-raw-source="[&lt;strong&gt;PAGED_CODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)"><strong>PAGED_CODE</strong></a>を呼び出すことができないように指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-reservedddis.md" data-raw-source="[&lt;strong&gt;ReservedDDIs&lt;/strong&gt;](wdm-reservedddis.md)"><strong>ReservedDDIs</strong></a></p></td>
<td align="left"><p><a href="wdm-reservedddis.md" data-raw-source="[&lt;strong&gt;ReservedDDIs&lt;/strong&gt;](wdm-reservedddis.md)"><strong>ReservedDDIs</strong></a>ルールは、ドライバーが予約されている関数を呼び出さないことを確認します。</p></td>
</tr>
</tbody>
</table>

 

**警告ルールセットを選択するには**

1.  Microsoft Visual Studio でドライバープロジェクト (.Vcxproj) を選択します。 **[ドライバー]** メニューの **[静的ドライバー検証ツールの起動]** をクリックします。

2.  **[ルール]** タブをクリックします。 **[ルールセット]** で **[警告]** を選択します。

    Visual Studio 開発者コマンドプロンプトウィンドウから既定の規則セットを選択するには、 **/チェック**オプションを指定して**Warning. sdv**を指定します。 次に、例を示します。

    ```
    msbuild /t:sdv /p:Inputs="/check:Warning.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    詳細については、「 [Using Static Driver verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers) 」を参照して、ドライバーと[静的ドライバー検証コマンド (MSBuild)](https://docs.microsoft.com/windows-hardware/drivers/devtest/-static-driver-verifier-commands--msbuild-)で欠陥を検出してください。

 

 





