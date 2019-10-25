---
title: Irql の規則セット (WDM)
description: これらのルールを使用して、ドライバーが必要な IRQL で DDI 呼び出しを行うことを確認します。IRQL 規則に従っていないドライバーは、デッドロック状態またはコンピューターのクラッシュにつながる可能性がある操作中に重大な問題を引き起こす可能性があります。
ms.assetid: 40C17906-58D5-4023-A549-0164C3A92A06
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 34d26b55a78b14e0659a1770220d1456c381356c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840254"
---
# <a name="irql-rule-set-wdm"></a>Irql の規則セット (WDM)


これらのルールを使用して、ドライバーが必要な IRQL で DDI 呼び出しを行うことを確認します。

IRQL 規則に従っていないドライバーは、デッドロック状態またはコンピューターのクラッシュにつながる可能性がある操作中に重大な問題を引き起こす可能性があります。

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
<td align="left"><p><a href="wdm-forwardedatbadirql.md" data-raw-source="[&lt;strong&gt;ForwardedAtBadIrql&lt;/strong&gt;](wdm-forwardedatbadirql.md)"><strong>ForwardedAtBadIrql</strong></a></p></td>
<td align="left"><p><a href="wdm-forwardedatbadirql.md" data-raw-source="[&lt;strong&gt;ForwardedAtBadIrql&lt;/strong&gt;](wdm-forwardedatbadirql.md)"><strong>ForwardedAtBadIrql</strong></a>規則は、転送される IRP メジャー関数コードが次のいずれかの場合を除き、ドライバーが IRQL&lt;DISPATCH_LEVEL で<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)"><strong>IoCallDriver</strong></a>と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver" data-raw-source="[&lt;strong&gt;PoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)"><strong>pocalldriver</strong></a>を呼び出す必要があることを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-forwardedatbadirqlallocate.md" data-raw-source="[&lt;strong&gt;ForwardedAtBadIrqlAllocate&lt;/strong&gt;](wdm-forwardedatbadirqlallocate.md)"><strong>ForwardedAtBadIrqlAllocate</strong></a></p></td>
<td align="left"><p><a href="wdm-forwardedatbadirqlallocate.md" data-raw-source="[&lt;strong&gt;ForwardedAtBadIrqlAllocate&lt;/strong&gt;](wdm-forwardedatbadirqlallocate.md)"><strong>ForwardedAtBadIrqlAllocate</strong></a>規則は、転送される IRP メジャー関数コードが次のいずれかの場合を除き、ドライバーが IRQL&lt;DISPATCH_LEVEL で<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)"><strong>IoCallDriver</strong></a>と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver" data-raw-source="[&lt;strong&gt;PoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)"><strong>pocalldriver</strong></a>を呼び出す必要があることを指定します。</p>
<ul>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power" data-raw-source="[&lt;strong&gt;IRP_MJ_POWER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)"><strong>IRP_MJ_POWER</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read" data-raw-source="[&lt;strong&gt;IRP_MJ_READ&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)"><strong>IRP_MJ_READ</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write" data-raw-source="[&lt;strong&gt;IRP_MJ_WRITE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)"><strong>IRP_MJ_WRITE</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control" data-raw-source="[&lt;strong&gt;IRP_MJ_DEVICE_CONTROL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)"><strong>IRP_MJ_DEVICE_CONTROL</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control" data-raw-source="[&lt;strong&gt;IRP_MJ_INTERNAL_DEVICE_CONTROL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)"><strong>IRP_MJ_INTERNAL_DEVICE_CONTROL</strong></a></li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-forwardedatbadirqlfsdasync.md" data-raw-source="[&lt;strong&gt;ForwardedAtBadIrqlFsdAsync&lt;/strong&gt;](wdm-forwardedatbadirqlfsdasync.md)"><strong>ForwardedAtBadIrqlFsdAsync</strong></a></p></td>
<td align="left"><p><a href="wdm-forwardedatbadirqlfsdasync.md" data-raw-source="[&lt;strong&gt;ForwardedAtBadIrqlFsdAsync&lt;/strong&gt;](wdm-forwardedatbadirqlfsdasync.md)"><strong>ForwardedAtBadIrqlFsdAsync</strong></a>規則は、転送される IRP メジャー関数コードが次のいずれかの場合を除き、ドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)"><strong>IoCallDriver</strong></a>と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver" data-raw-source="[&lt;strong&gt;PoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)"><strong>pocalldriver</strong></a>を IRQL&lt;DISPATCH_LEVEL に呼び出すことを指定します。</p>
<ul>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power" data-raw-source="[&lt;strong&gt;IRP_MJ_POWER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)"><strong>IRP_MJ_POWER</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read" data-raw-source="[&lt;strong&gt;IRP_MJ_READ&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)"><strong>IRP_MJ_READ</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write" data-raw-source="[&lt;strong&gt;IRP_MJ_WRITE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)"><strong>IRP_MJ_WRITE</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control" data-raw-source="[&lt;strong&gt;IRP_MJ_DEVICE_CONTROL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)"><strong>IRP_MJ_DEVICE_CONTROL</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control" data-raw-source="[&lt;strong&gt;IRP_MJ_INTERNAL_DEVICE_CONTROL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)"><strong>IRP_MJ_INTERNAL_DEVICE_CONTROL</strong></a></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-forwardedatbadirqlfsdsync.md" data-raw-source="[&lt;strong&gt;ForwardedAtBadIrqlFsdSync&lt;/strong&gt;](wdm-forwardedatbadirqlfsdsync.md)"><strong>ForwardedAtBadIrqlFsdSync</strong></a></p></td>
<td align="left"><p><a href="wdm-forwardedatbadirqlfsdsync.md" data-raw-source="[&lt;strong&gt;ForwardedAtBadIrqlFsdSync&lt;/strong&gt;](wdm-forwardedatbadirqlfsdsync.md)"><strong>ForwardedAtBadIrqlFsdSync</strong></a>規則は、転送される IRP メジャー関数コードが次のいずれかの場合を除き、ドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)"><strong>IoCallDriver</strong></a>と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver" data-raw-source="[&lt;strong&gt;PoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)"><strong>pocalldriver</strong></a>を IRQL&lt;DISPATCH_LEVEL に呼び出すことを指定します。</p>
<ul>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power" data-raw-source="[&lt;strong&gt;IRP_MJ_POWER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)"><strong>IRP_MJ_POWER</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read" data-raw-source="[&lt;strong&gt;IRP_MJ_READ&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)"><strong>IRP_MJ_READ</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write" data-raw-source="[&lt;strong&gt;IRP_MJ_WRITE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)"><strong>IRP_MJ_WRITE</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control" data-raw-source="[&lt;strong&gt;IRP_MJ_DEVICE_CONTROL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)"><strong>IRP_MJ_DEVICE_CONTROL</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control" data-raw-source="[&lt;strong&gt;IRP_MJ_INTERNAL_DEVICE_CONTROL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)"><strong>IRP_MJ_INTERNAL_DEVICE_CONTROL</strong></a></li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlapclte.md" data-raw-source="[&lt;strong&gt;IrqlApcLte&lt;/strong&gt;](wdm-irqlapclte.md)"><strong>IrqlApcLte</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlapclte.md" data-raw-source="[&lt;strong&gt;IrqlApcLte&lt;/strong&gt;](wdm-irqlapclte.md)"><strong>IrqlApcLte</strong></a>規則は、ドライバーが IRQL &lt;= APC_LEVEL で実行されている場合にのみ、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obgetobjectsecurity" data-raw-source="[&lt;strong&gt;ObGetObjectSecurity&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obgetobjectsecurity)"><strong>obgetobjectsecurity</strong></a>および<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreleaseobjectsecurity" data-raw-source="[&lt;strong&gt;ObReleaseObjectSecurity&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreleaseobjectsecurity)"><strong>obgetobjectsecurity</strong></a>を呼び出すように指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqldispatch.md" data-raw-source="[&lt;strong&gt;IrqlDispatch&lt;/strong&gt;](wdm-irqldispatch.md)"><strong>IrqlDispatch</strong></a></p></td>
<td align="left"><p><a href="wdm-irqldispatch.md" data-raw-source="[&lt;strong&gt;IrqlDispatch&lt;/strong&gt;](wdm-irqldispatch.md)"><strong>Irqldispatch</strong></a>ルールでは、ドライバーが IRQL = DISPATCH_LEVEL で実行されている場合にのみ、次の DDIs を呼び出すように指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlexallocatepool.md" data-raw-source="[&lt;strong&gt;IrqlExAllocatePool&lt;/strong&gt;](wdm-irqlexallocatepool.md)"><strong>IrqlExAllocatePool</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlexallocatepool.md" data-raw-source="[&lt;strong&gt;IrqlExAllocatePool&lt;/strong&gt;](wdm-irqlexallocatepool.md)"><strong>IrqlExAllocatePool</strong></a>規則は、IRQL&lt;= DISPATCH_LEVEL で実行されている場合にのみ、ドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag" data-raw-source="[&lt;strong&gt;ExAllocatePoolWithTag&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)"><strong>Exallocatepoolwithtag</strong></a>と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtagpriority" data-raw-source="[&lt;strong&gt;ExAllocatePoolWithTagPriority&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtagpriority)"><strong>Exallocatepoolwithtagpriority</strong></a>を呼び出すように指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqlexapclte1.md" data-raw-source="[&lt;strong&gt;IrqlExApcLte1&lt;/strong&gt;](wdm-irqlexapclte1.md)"><strong>IrqlExApcLte1</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlexapclte1.md" data-raw-source="[&lt;strong&gt;IrqlExApcLte1&lt;/strong&gt;](wdm-irqlexapclte1.md)"><strong>IrqlExApcLte1</strong></a>規則は、ドライバーが<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff544337(v=vs.85)" data-raw-source="[&lt;strong&gt;ExAcquireFastMutex&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff544337(v=vs.85))"><strong>ExAcquireFastMutex</strong></a>と<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545647(v=vs.85)" data-raw-source="[&lt;strong&gt;ExTryToAcquireFastMutex&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545647(v=vs.85))"><strong>ExTryToAcquireFastMutex</strong></a>を呼び出すことを指定します。これは、IRQL &lt;= APC_LEVEL でのみ行います。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlexapclte2.md" data-raw-source="[&lt;strong&gt;IrqlExApcLte2&lt;/strong&gt;](wdm-irqlexapclte2.md)"><strong>IrqlExApcLte2</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlexapclte2.md" data-raw-source="[&lt;strong&gt;IrqlExApcLte2&lt;/strong&gt;](wdm-irqlexapclte2.md)"><strong>IrqlExApcLte2</strong></a>規則は、ドライバーが IRQL &lt;= APC_LEVEL でのみ次のルーチンを呼び出すことを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqlexapclte3.md" data-raw-source="[&lt;strong&gt;IrqlExApcLte3&lt;/strong&gt;](wdm-irqlexapclte3.md)"><strong>IrqlExApcLte3</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlexapclte3.md" data-raw-source="[&lt;strong&gt;IrqlExApcLte3&lt;/strong&gt;](wdm-irqlexapclte3.md)"><strong>IrqlExApcLte3</strong></a>ルールは、ドライバーが IRQL &lt;= APC_LEVEL でのみ次の executive サポートルーチンを呼び出すことを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlexapclteinline.md" data-raw-source="[&lt;strong&gt;IrqlExApcLteInline&lt;/strong&gt;](wdm-irqlexapclteinline.md)"><strong>IrqlExApcLteInline</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlexapclteinline.md" data-raw-source="[&lt;strong&gt;IrqlExApcLteInline&lt;/strong&gt;](wdm-irqlexapclteinline.md)"><strong>IrqlExApcLteInline</strong></a>ルールは、DDIs が適切な IRQL レベルでのみ呼び出されることを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqlexfree1.md" data-raw-source="[&lt;strong&gt;IrqlExFree1&lt;/strong&gt;](wdm-irqlexfree1.md)"><strong>IrqlExFree1</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlexfree1.md" data-raw-source="[&lt;strong&gt;IrqlExFree1&lt;/strong&gt;](wdm-irqlexfree1.md)"><strong>IrqlExFree1</strong></a>ルールでは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool" data-raw-source="[&lt;strong&gt;ExFreePool&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool)"><strong>exfreepool</strong></a>と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exfreepoolwithtag" data-raw-source="[&lt;strong&gt;ExFreePoolWithTag&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exfreepoolwithtag)"><strong>exfreepoolwithtag</strong></a>が適切な IRQL で呼び出されることを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlexfree2.md" data-raw-source="[&lt;strong&gt;IrqlExFree2&lt;/strong&gt;](wdm-irqlexfree2.md)"><strong>IrqlExFree2</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlexfree2.md" data-raw-source="[&lt;strong&gt;IrqlExFree2&lt;/strong&gt;](wdm-irqlexfree2.md)"><strong>IrqlExFree2</strong></a>ルールでは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool" data-raw-source="[&lt;strong&gt;ExFreePool&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool)"><strong>exfreepool</strong></a>と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exfreepoolwithtag" data-raw-source="[&lt;strong&gt;ExFreePoolWithTag&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exfreepoolwithtag)"><strong>exfreepoolwithtag</strong></a>が適切な IRQL で呼び出されることを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqlexfree3.md" data-raw-source="[&lt;strong&gt;IrqlExFree3&lt;/strong&gt;](wdm-irqlexfree3.md)"><strong>IrqlExFree3</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlexfree3.md" data-raw-source="[&lt;strong&gt;IrqlExFree3&lt;/strong&gt;](wdm-irqlexfree3.md)"><strong>IrqlExFree3</strong></a>ルールでは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool" data-raw-source="[&lt;strong&gt;ExFreePool&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool)"><strong>exfreepool</strong></a>と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exfreepoolwithtag" data-raw-source="[&lt;strong&gt;ExFreePoolWithTag&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exfreepoolwithtag)"><strong>exfreepoolwithtag</strong></a>が適切な IRQL で呼び出されることを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlexpassive.md" data-raw-source="[&lt;strong&gt;IrqlExPassive&lt;/strong&gt;](wdm-irqlexpassive.md)"><strong>IrqlExPassive</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlexpassive.md" data-raw-source="[&lt;strong&gt;IrqlExPassive&lt;/strong&gt;](wdm-irqlexpassive.md)"><strong>IrqlExPassive</strong></a>規則は、ドライバーが次の executive サポートルーチンを呼び出すことを指定します。 IRQL = PASSIVE_LEVEL:</p>
<ul>
<li><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-excreatecallback" data-raw-source="[&lt;strong&gt;ExCreateCallback&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-excreatecallback)"><strong>ExCreateCallback</strong></a></p></li>
<li><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exisprocessorfeaturepresent" data-raw-source="[&lt;strong&gt;ExIsProcessorFeaturePresent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exisprocessorfeaturepresent)"><strong>ExIsProcessorFeaturePresent</strong></a></p></li>
<li><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exraiseaccessviolation" data-raw-source="[&lt;strong&gt;ExRaiseAccessViolation&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exraiseaccessviolation)"><strong>ExRaiseAccessViolation</strong></a></p></li>
<li><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exraisedatatypemisalignment" data-raw-source="[&lt;strong&gt;ExRaiseDatatypeMisalignment&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exraisedatatypemisalignment)"><strong>ExRaiseDatatypeMisalignment</strong></a></p></li>
<li><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exraisestatus" data-raw-source="[&lt;strong&gt;ExRaiseStatus&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exraisestatus)"><strong>ExRaiseStatus</strong></a></p></li>
<li><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exuuidcreate" data-raw-source="[&lt;strong&gt;ExUuidCreate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exuuidcreate)"><strong>ExUuidCreate</strong></a></p></li>
</ul>
<p>また、 <a href="wdm-irqlexpassive.md" data-raw-source="[&lt;strong&gt;IrqlExPassive&lt;/strong&gt;](wdm-irqlexpassive.md)"><strong>IrqlExPassive</strong></a>ルールでは、ドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exraisestatus" data-raw-source="[&lt;strong&gt;ExRaiseStatus&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exraisestatus)"><strong>ExRaiseStatus</strong></a>を呼び出すように指定しています &lt;= APC_LEVEL</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqlioapclte.md" data-raw-source="[&lt;strong&gt;IrqlIoApcLte&lt;/strong&gt;](wdm-irqlioapclte.md)"><strong>IrqlIoApcLte</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlioapclte.md" data-raw-source="[&lt;strong&gt;IrqlIoApcLte&lt;/strong&gt;](wdm-irqlioapclte.md)"><strong>IrqlIoApcLte</strong></a>規則は、ドライバーが IRQL &lt;= APC_LEVEL で実行されている場合にのみ、次の i/o マネージャールーチンを呼び出すように指定します。</p>
<ul>
<li><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodeletedevice" data-raw-source="[&lt;strong&gt;IoDeleteDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodeletedevice)"><strong>IoDeleteDevice</strong></a></p></li>
<li><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetinitialstack" data-raw-source="[&lt;strong&gt;IoGetInitialStack&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetinitialstack)"><strong>IoGetInitialStack</strong></a></p></li>
<li><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioraiseharderror" data-raw-source="[&lt;strong&gt;IoRaiseHardError&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioraiseharderror)"><strong>IoRaiseHardError</strong></a></p></li>
<li><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioraiseinformationalharderror" data-raw-source="[&lt;strong&gt;IoRaiseInformationalHardError&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioraiseinformationalharderror)"><strong>IoRaiseInformationalHardError</strong></a></p></li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqliodispatch.md" data-raw-source="[&lt;strong&gt;IrqlIoDispatch&lt;/strong&gt;](wdm-irqliodispatch.md)"><strong>IrqlIoDispatch</strong></a></p></td>
<td align="left"><p><a href="wdm-irqliodispatch.md" data-raw-source="[&lt;strong&gt;IrqlIoDispatch&lt;/strong&gt;](wdm-irqliodispatch.md)"><strong>IrqlIoDispatch</strong></a>規則は、ドライバーが IRQL &lt;= DISPATCH_LEVEL: <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iogetdevicetoverify" data-raw-source="[&lt;strong&gt;IoGetDeviceToVerify&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iogetdevicetoverify)"><strong>iogetdevicetoverify</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iosetdevicetoverify" data-raw-source="[&lt;strong&gt;IoSetDeviceToVerify&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iosetdevicetoverify)"><strong>iogetdevicetoverify</strong></a>で実行されている場合にのみ、次の i/o マネージャールーチンを呼び出すように指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqliopassive1.md" data-raw-source="[&lt;strong&gt;IrqlIoPassive1&lt;/strong&gt;](wdm-irqliopassive1.md)"><strong>IrqlIoPassive1</strong></a></p></td>
<td align="left"><p><a href="wdm-irqliopassive1.md" data-raw-source="[&lt;strong&gt;IrqlIoPassive1&lt;/strong&gt;](wdm-irqliopassive1.md)"><strong>IrqlIoPassive1</strong></a>規則は、ドライバーが IRQL = PASSIVE_LEVEL で実行されている場合にのみ、次のルーチンを呼び出すように指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqliopassive2.md" data-raw-source="[&lt;strong&gt;IrqlIoPassive2&lt;/strong&gt;](wdm-irqliopassive2.md)"><strong>IrqlIoPassive2</strong></a></p></td>
<td align="left"><p><a href="wdm-irqliopassive2.md" data-raw-source="[&lt;strong&gt;IrqlIoPassive2&lt;/strong&gt;](wdm-irqliopassive2.md)"><strong>IrqlIoPassive2</strong></a>規則は、ドライバーが次の i/o マネージャールーチンを IRQL = PASSIVE_LEVEL でのみ呼び出すことを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqliopassive3.md" data-raw-source="[&lt;strong&gt;IrqlIoPassive3&lt;/strong&gt;](wdm-irqliopassive3.md)"><strong>IrqlIoPassive3</strong></a></p></td>
<td align="left"><p>IrqlIoPassive3 規則は、ドライバーが IRQL = PASSIVE_LEVEL で実行されている場合にのみ、次のルーチンを呼び出すように指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqliopassive4.md" data-raw-source="[&lt;strong&gt;IrqlIoPassive4&lt;/strong&gt;](wdm-irqliopassive4.md)"><strong>IrqlIoPassive4</strong></a></p></td>
<td align="left"><p><a href="wdm-irqliopassive4.md" data-raw-source="[&lt;strong&gt;IrqlIoPassive4&lt;/strong&gt;](wdm-irqliopassive4.md)"><strong>IrqlIoPassive4</strong></a>規則は、ドライバーが IRQL = PASSIVE_LEVEL で実行されている場合にのみ、次のルーチンを呼び出すように指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqliopassive5.md" data-raw-source="[&lt;strong&gt;IrqlIoPassive5&lt;/strong&gt;](wdm-irqliopassive5.md)"><strong>IrqlIoPassive5</strong></a></p></td>
<td align="left"><p><a href="wdm-irqliopassive5.md" data-raw-source="[&lt;strong&gt;IrqlIoPassive5&lt;/strong&gt;](wdm-irqliopassive5.md)"><strong>IrqlIoPassive5</strong></a>規則は、ドライバーが IRQL = PASSIVE_LEVEL で実行されている場合にのみ、特定の i/o マネージャールーチンを呼び出すように指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlkeapclte1.md" data-raw-source="[&lt;strong&gt;IrqlKeApcLte1&lt;/strong&gt;](wdm-irqlkeapclte1.md)"><strong>IrqlKeApcLte1</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlkeapclte1.md" data-raw-source="[&lt;strong&gt;IrqlKeApcLte1&lt;/strong&gt;](wdm-irqlkeapclte1.md)"><strong>IrqlKeApcLte1</strong></a>規則は、ドライバーが IRQL &lt;= APC_LEVEL で実行されている場合にのみ、次のカーネルルーチンを呼び出すように指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqlkeapclte2.md" data-raw-source="[&lt;strong&gt;IrqlKeApcLte2&lt;/strong&gt;](wdm-irqlkeapclte2.md)"><strong>IrqlKeApcLte2</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlkeapclte2.md" data-raw-source="[&lt;strong&gt;IrqlKeApcLte2&lt;/strong&gt;](wdm-irqlkeapclte2.md)"><strong>IrqlKeApcLte2</strong></a>規則は、ドライバーが IRQL &lt;= APC_LEVEL で実行されている場合にのみ、次のカーネルルーチンを呼び出すように指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlkedispatchlte.md" data-raw-source="[&lt;strong&gt;IrqlKeDispatchLte&lt;/strong&gt;](wdm-irqlkedispatchlte.md)"><strong>IrqlKeDispatchLte</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlkedispatchlte.md" data-raw-source="[&lt;strong&gt;IrqlKeDispatchLte&lt;/strong&gt;](wdm-irqlkedispatchlte.md)"><strong>IrqlKeDispatchLte</strong></a>規則は、ドライバーが IRQL &lt;= DISPATCH_LEVEL で実行されている場合にのみ、次のカーネルルーチンを呼び出すように指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqlkeraiselower.md" data-raw-source="[&lt;strong&gt;IrqlKeRaiseLower&lt;/strong&gt;](wdm-irqlkeraiselower.md)"><strong>IrqlKeRaiseLower</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlkeraiselower" data-raw-source="[&lt;strong&gt;IrqlKeRaiseLower&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlkeraiselower)"><strong>Irqlkeraiselower</strong></a>ルールでは、IRQL を上げたり下げたりするときに、ドライバーが次のことを実行することを指定します。</p>
ドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keraiseirql" data-raw-source="[&lt;strong&gt;KeRaiseIrql&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keraiseirql)"><strong>Keraiseirql</strong></a>を呼び出すと、 <em>NewIrql</em>パラメーターの値以下の irql で実行されます。<br />
ドライバーは、 <strong>Keraiseirql</strong>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keraiseirqltodpclevel" data-raw-source="[&lt;strong&gt;KeRaiseIrqlToDpcLevel&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keraiseirqltodpclevel)"><strong>KeRaiseIrqlToDpcLevel</strong></a>を呼び出した後にのみ<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kelowerirql" data-raw-source="[&lt;strong&gt;KeLowerIrql&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kelowerirql)"><strong>kelowerirql</strong></a>を呼び出します。<br />
</td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlkeraiselower2.md" data-raw-source="[&lt;strong&gt;IrqlKeRaiseLower2&lt;/strong&gt;](wdm-irqlkeraiselower2.md)"><strong>IrqlKeRaiseLower2</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlkeraiselower2.md" data-raw-source="[&lt;strong&gt;IrqlKeRaiseLower2&lt;/strong&gt;](wdm-irqlkeraiselower2.md)"><strong>IrqlKeRaiseLower2</strong></a>ルールは、ドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kelowerirql" data-raw-source="[&lt;strong&gt;KeLowerIrql&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kelowerirql)"><strong>ke irql</strong></a>を使用して、以前の<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keraiseirql" data-raw-source="[&lt;strong&gt;KeRaiseIrql&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keraiseirql)"><strong>Keraiseirql</strong></a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keraiseirqltodpclevel" data-raw-source="[&lt;strong&gt;KeRaiseIrqlToDpcLevel&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keraiseirqltodpclevel)"><strong>KeRaiseIrqlToDpcLevel</strong></a>の呼び出しによって発生した元の irql を復元するように指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqlkereleasespinlock.md" data-raw-source="[&lt;strong&gt;IrqlKeReleaseSpinLock&lt;/strong&gt;](wdm-irqlkereleasespinlock.md)"><strong>IrqlKeReleaseSpinLock</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlkereleasespinlock.md" data-raw-source="[&lt;strong&gt;IrqlKeReleaseSpinLock&lt;/strong&gt;](wdm-irqlkereleasespinlock.md)"><strong>IrqlKeReleaseSpinLock</strong></a>規則は、IRQL = DISPATCH_LEVEL で実行されている場合にのみ、ドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock" data-raw-source="[&lt;strong&gt;KeReleaseSpinLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock)"><strong>KeReleaseSpinLock</strong></a>を呼び出すことを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlkesetevent.md" data-raw-source="[&lt;strong&gt;IrqlKeSetEvent&lt;/strong&gt;](wdm-irqlkesetevent.md)"><strong>IrqlKeSetEvent</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlkesetevent.md" data-raw-source="[&lt;strong&gt;IrqlKeSetEvent&lt;/strong&gt;](wdm-irqlkesetevent.md)"><strong>IrqlKeSetEvent</strong></a>ルールは、Wait が<strong>FALSE</strong>に設定されて<em>いる場合は</em>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent" data-raw-source="[&lt;strong&gt;KeSetEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent)"><strong>KeSetEvent</strong></a>ルーチンが irql &lt;= DISPATCH_LEVEL でのみ呼び出されることを指定し、 <em>wait</em>が<strong>TRUE</strong>に設定されている場合は、irql &lt;= APC_LEVEL を呼び出します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqlkewaitformutexobject.md" data-raw-source="[&lt;strong&gt;IrqlKeWaitForMutexObject&lt;/strong&gt;](wdm-irqlkewaitformutexobject.md)"><strong>IrqlKeWaitForMutexObject</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlkewaitformutexobject.md" data-raw-source="[&lt;strong&gt;IrqlKeWaitForMutexObject&lt;/strong&gt;](wdm-irqlkewaitformutexobject.md)"><strong>Irqlkewaitformutexobject</strong></a>ルールでは、 <em>Timeout</em>パラメーターの値に基づいて、適切な IRQL で<a href="https://msdn.microsoft.com/library/windows/hardware/ff553344" data-raw-source="[&lt;strong&gt;KeWaitForMutexObject&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553344)"><strong>kewaitformutexobject</strong></a>ルーチンを呼び出すようにドライバーを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlkewaitformultipleobjects.md" data-raw-source="[&lt;strong&gt;IrqlKeWaitForMultipleObjects&lt;/strong&gt;](wdm-irqlkewaitformultipleobjects.md)"><strong>IrqlKeWaitForMultipleObjects</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlkewaitformultipleobjects.md" data-raw-source="[&lt;strong&gt;IrqlKeWaitForMultipleObjects&lt;/strong&gt;](wdm-irqlkewaitformultipleobjects.md)"><strong>IrqlKeWaitForMultipleObjects</strong></a>規則は、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitformultipleobjects" data-raw-source="[&lt;strong&gt;KeWaitForMultipleObjects&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitformultipleobjects)"><strong>KeWaitForMultipleObjects</strong></a>ルーチンの呼び出し元が、 <em>Timeout</em>パラメーターに基づいて適切な IRQL で実行されている必要があることを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqlmmapclte.md" data-raw-source="[&lt;strong&gt;IrqlMmApcLte&lt;/strong&gt;](wdm-irqlmmapclte.md)"><strong>IrqlMmApcLte</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlmmapclte.md" data-raw-source="[&lt;strong&gt;IrqlMmApcLte&lt;/strong&gt;](wdm-irqlmmapclte.md)"><strong>Irqlmmapclte</strong></a>ルールでは、ドライバーが IRQL &lt;= APC_LEVEL で実行されている場合にのみ、次のメモリマネージャールーチンを呼び出すように指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlmmdispatch.md" data-raw-source="[&lt;strong&gt;IrqlMmDispatch&lt;/strong&gt;](wdm-irqlmmdispatch.md)"><strong>IrqlMmDispatch</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlmmdispatch.md" data-raw-source="[&lt;strong&gt;IrqlMmDispatch&lt;/strong&gt;](wdm-irqlmmdispatch.md)"><strong>Irqlmmdispatch</strong></a>ルールでは、ドライバーが<strong>IRQL &lt;= DISPATCH_LEVEL</strong>で実行されている場合にのみ<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmfreecontiguousmemory" data-raw-source="[&lt;strong&gt;MmFreeContiguousMemory&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmfreecontiguousmemory)"><strong>MmFreeContiguousMemory</strong></a>を呼び出すように指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqlobpassive.md" data-raw-source="[&lt;strong&gt;IrqlObPassive&lt;/strong&gt;](wdm-irqlobpassive.md)"><strong>IrqlObPassive</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlobpassive.md" data-raw-source="[&lt;strong&gt;IrqlObPassive&lt;/strong&gt;](wdm-irqlobpassive.md)"><strong>IrqlObPassive</strong></a>規則は、IRQL = PASSIVE_LEVEL で実行されている場合にのみ、ドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle" data-raw-source="[&lt;strong&gt;ObReferenceObjectByHandle&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle)"><strong>Obreferenceobjectbyhandle</strong></a>を呼び出すように指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlpspassive.md" data-raw-source="[&lt;strong&gt;IrqlPsPassive&lt;/strong&gt;](wdm-irqlpspassive.md)"><strong>IrqlPsPassive</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlpspassive.md" data-raw-source="[&lt;strong&gt;IrqlPsPassive&lt;/strong&gt;](wdm-irqlpspassive.md)"><strong>IrqlPsPassive</strong></a>規則は、ドライバーが IRQL = PASSIVE_LEVEL で実行されている場合にのみ、次の<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/index" data-raw-source="[&lt;strong&gt;Process Structure routines&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)"><strong>プロセス構造ルーチン</strong></a>を呼び出すように指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqlreturn.md" data-raw-source="[&lt;strong&gt;IrqlReturn&lt;/strong&gt;](wdm-irqlreturn.md)"><strong>IrqlReturn</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlreturn.md" data-raw-source="[&lt;strong&gt;IrqlReturn&lt;/strong&gt;](wdm-irqlreturn.md)"><strong>Irqlreturn</strong></a>ルールでは、ドライバーのディスパッチルーチンが、呼び出されたときと同じ IRQL で返されることを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlrtlpassive.md" data-raw-source="[&lt;strong&gt;IrqlRtlPassive&lt;/strong&gt;](wdm-irqlrtlpassive.md)"><strong>IrqlRtlPassive</strong></a></p></td>
<td align="left"><p>IrqlRtlPassive 規則は、IRQL = PASSIVE_LEVEL で実行されている場合にのみ、ドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtldeleteregistryvalue" data-raw-source="[&lt;strong&gt;RtlDeleteRegistryValue&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtldeleteregistryvalue)"><strong>RtlDeleteRegistryValue</strong></a>を呼び出すことを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqlzwpassive.md" data-raw-source="[&lt;strong&gt;IrqlZwPassive&lt;/strong&gt;](wdm-irqlzwpassive.md)"><strong>IrqlZwPassive</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlzwpassive.md" data-raw-source="[&lt;strong&gt;IrqlZwPassive&lt;/strong&gt;](wdm-irqlzwpassive.md)"><strong>IrqlZwPassive</strong></a>規則は、ドライバーが IRQL = PASSIVE_LEVEL で実行されている場合にのみ<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose" data-raw-source="[&lt;strong&gt;ZwClose&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)"><strong>zwclose</strong></a>を呼び出すように指定します。</p></td>
</tr>
</tbody>
</table>

 

**Irql 規則セットを選択するには**

1.  Microsoft Visual Studio でドライバープロジェクト (.Vcxproj) を選択します。 **[ドライバー]** メニューの **[静的ドライバー検証ツールの起動]** をクリックします。

2.  **[ルール]** タブをクリックします。 **[規則セット]** で **[Irql]** を選択します。

    Visual Studio 開発者コマンドプロンプトウィンドウから既定の規則セットを選択するには、 **/チェック**オプションを指定して、 **Irql**を指定します。 次に、例を示します。

    ```
    msbuild /t:sdv /p:Inputs="/check:Irql.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    詳細については、「 [Using Static Driver verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers) 」を参照して、ドライバーと[静的ドライバー検証コマンド (MSBuild)](https://docs.microsoft.com/windows-hardware/drivers/devtest/-static-driver-verifier-commands--msbuild-)で欠陥を検出してください。

 

 





