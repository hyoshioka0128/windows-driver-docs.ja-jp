---
title: Irql の規則セット (WDM)
description: これらの規則を使用すると、ドライバーが必要な IRQL で DDI 呼び出しを行うことを確認します。IRQL の規則に従っていないドライバーは、デッドロック状態またはコンピューターがクラッシュする可能性のある操作中に重大な問題を発生することができます。
ms.assetid: 40C17906-58D5-4023-A549-0164C3A92A06
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1af49b04086b4c5cc01616658619990240543858
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340450"
---
# <a name="irql-rule-set-wdm"></a>Irql の規則セット (WDM)


これらの規則を使用すると、ドライバーが必要な IRQL で DDI 呼び出しを行うことを確認します。

IRQL の規則に従っていないドライバーは、デッドロック状態またはコンピューターがクラッシュする可能性のある操作中に重大な問題を発生することができます。

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
<td align="left"><p><a href="wdm-forwardedatbadirql.md" data-raw-source="[&lt;strong&gt;ForwardedAtBadIrql&lt;/strong&gt;](wdm-forwardedatbadirql.md)"> <strong>ForwardedAtBadIrql</strong> </a>ルールでは、ドライバーを呼び出す必要がありますを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff548336" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548336)"><strong>保留</strong></a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff559654" data-raw-source="[&lt;strong&gt;PoCallDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559654)"> <strong>PoCallDriver</strong> </a> IRQL で&lt;DISPATCH_LEVEL は IRP の主要な関数のコードが転送されていない場合は、次のいずれか。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-forwardedatbadirqlallocate.md" data-raw-source="[&lt;strong&gt;ForwardedAtBadIrqlAllocate&lt;/strong&gt;](wdm-forwardedatbadirqlallocate.md)"><strong>ForwardedAtBadIrqlAllocate</strong></a></p></td>
<td align="left"><p><a href="wdm-forwardedatbadirqlallocate.md" data-raw-source="[&lt;strong&gt;ForwardedAtBadIrqlAllocate&lt;/strong&gt;](wdm-forwardedatbadirqlallocate.md)"> <strong>ForwardedAtBadIrqlAllocate</strong> </a>ルールでは、ドライバーを呼び出す必要がありますを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff548336" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548336)"><strong>保留</strong></a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff559654" data-raw-source="[&lt;strong&gt;PoCallDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559654)"> <strong>PoCallDriver</strong> </a> IRQL で&lt;DISPATCH_LEVEL は IRP の主要な関数のコードが転送されていない場合は、次のいずれか。</p>
<ul>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/ff550784" data-raw-source="[&lt;strong&gt;IRP_MJ_POWER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550784)"><strong>IRP_MJ_POWER</strong></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/ff550794" data-raw-source="[&lt;strong&gt;IRP_MJ_READ&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550794)"><strong>IRP_MJ_READ</strong></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/ff550819" data-raw-source="[&lt;strong&gt;IRP_MJ_WRITE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550819)"><strong>IRP_MJ_WRITE</strong></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/ff550744" data-raw-source="[&lt;strong&gt;IRP_MJ_DEVICE_CONTROL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550744)"><strong>IRP_MJ_DEVICE_CONTROL</strong></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/ff550766" data-raw-source="[&lt;strong&gt;IRP_MJ_INTERNAL_DEVICE_CONTROL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550766)"><strong>IRP_MJ_INTERNAL_DEVICE_CONTROL</strong></a></li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-forwardedatbadirqlfsdasync.md" data-raw-source="[&lt;strong&gt;ForwardedAtBadIrqlFsdAsync&lt;/strong&gt;](wdm-forwardedatbadirqlfsdasync.md)"><strong>ForwardedAtBadIrqlFsdAsync</strong></a></p></td>
<td align="left"><p><a href="wdm-forwardedatbadirqlfsdasync.md" data-raw-source="[&lt;strong&gt;ForwardedAtBadIrqlFsdAsync&lt;/strong&gt;](wdm-forwardedatbadirqlfsdasync.md)"> <strong>ForwardedAtBadIrqlFsdAsync</strong> </a>ルールでは、ドライバーを呼び出すことを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff548336" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548336)"><strong>保留</strong></a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff559654" data-raw-source="[&lt;strong&gt;PoCallDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559654)"> <strong>PoCallDriver</strong> </a> IRQL で&lt;DISPATCH_LEVEL は IRP の主要な関数のコードが転送されていない場合は、次のいずれか。</p>
<ul>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/ff550784" data-raw-source="[&lt;strong&gt;IRP_MJ_POWER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550784)"><strong>IRP_MJ_POWER</strong></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/ff550794" data-raw-source="[&lt;strong&gt;IRP_MJ_READ&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550794)"><strong>IRP_MJ_READ</strong></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/ff550819" data-raw-source="[&lt;strong&gt;IRP_MJ_WRITE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550819)"><strong>IRP_MJ_WRITE</strong></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/ff550744" data-raw-source="[&lt;strong&gt;IRP_MJ_DEVICE_CONTROL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550744)"><strong>IRP_MJ_DEVICE_CONTROL</strong></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/ff550766" data-raw-source="[&lt;strong&gt;IRP_MJ_INTERNAL_DEVICE_CONTROL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550766)"><strong>IRP_MJ_INTERNAL_DEVICE_CONTROL</strong></a></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-forwardedatbadirqlfsdsync.md" data-raw-source="[&lt;strong&gt;ForwardedAtBadIrqlFsdSync&lt;/strong&gt;](wdm-forwardedatbadirqlfsdsync.md)"><strong>ForwardedAtBadIrqlFsdSync</strong></a></p></td>
<td align="left"><p><a href="wdm-forwardedatbadirqlfsdsync.md" data-raw-source="[&lt;strong&gt;ForwardedAtBadIrqlFsdSync&lt;/strong&gt;](wdm-forwardedatbadirqlfsdsync.md)"> <strong>ForwardedAtBadIrqlFsdSync</strong> </a>ルールでは、ドライバーを呼び出すことを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff548336" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548336)"><strong>保留</strong></a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff559654" data-raw-source="[&lt;strong&gt;PoCallDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559654)"> <strong>PoCallDriver</strong> </a> IRQL で&lt;DISPATCH_LEVEL は IRP の主要な関数のコードが転送されていない場合は、次のいずれか。</p>
<ul>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/ff550784" data-raw-source="[&lt;strong&gt;IRP_MJ_POWER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550784)"><strong>IRP_MJ_POWER</strong></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/ff550794" data-raw-source="[&lt;strong&gt;IRP_MJ_READ&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550794)"><strong>IRP_MJ_READ</strong></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/ff550819" data-raw-source="[&lt;strong&gt;IRP_MJ_WRITE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550819)"><strong>IRP_MJ_WRITE</strong></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/ff550744" data-raw-source="[&lt;strong&gt;IRP_MJ_DEVICE_CONTROL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550744)"><strong>IRP_MJ_DEVICE_CONTROL</strong></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/ff550766" data-raw-source="[&lt;strong&gt;IRP_MJ_INTERNAL_DEVICE_CONTROL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550766)"><strong>IRP_MJ_INTERNAL_DEVICE_CONTROL</strong></a></li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlapclte.md" data-raw-source="[&lt;strong&gt;IrqlApcLte&lt;/strong&gt;](wdm-irqlapclte.md)"><strong>IrqlApcLte</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlapclte.md" data-raw-source="[&lt;strong&gt;IrqlApcLte&lt;/strong&gt;](wdm-irqlapclte.md)"> <strong>IrqlApcLte</strong> </a>ルールでは、ドライバーを呼び出すことを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff557738" data-raw-source="[&lt;strong&gt;ObGetObjectSecurity&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557738)"> <strong>ObGetObjectSecurity</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff558695" data-raw-source="[&lt;strong&gt;ObReleaseObjectSecurity&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff558695)"> <strong>ObReleaseObjectSecurity</strong> </a> IRQL でその実行はときにのみ&lt;APC_LEVEL を = です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqldispatch.md" data-raw-source="[&lt;strong&gt;IrqlDispatch&lt;/strong&gt;](wdm-irqldispatch.md)"><strong>IrqlDispatch</strong></a></p></td>
<td align="left"><p><a href="wdm-irqldispatch.md" data-raw-source="[&lt;strong&gt;IrqlDispatch&lt;/strong&gt;](wdm-irqldispatch.md)"> <strong>IrqlDispatch</strong> </a>ルールでは、IRQL で実行されている場合にのみ、ドライバーが次の Ddi を呼び出すことを指定します = DISPATCH_LEVEL します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlexallocatepool.md" data-raw-source="[&lt;strong&gt;IrqlExAllocatePool&lt;/strong&gt;](wdm-irqlexallocatepool.md)"><strong>IrqlExAllocatePool</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlexallocatepool.md" data-raw-source="[&lt;strong&gt;IrqlExAllocatePool&lt;/strong&gt;](wdm-irqlexallocatepool.md)"> <strong>IrqlExAllocatePool</strong> </a>ルールでは、ドライバーを呼び出すことを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff544520" data-raw-source="[&lt;strong&gt;ExAllocatePoolWithTag&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544520)"> <strong>exallocatepoolwithtag に</strong></a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff544523" data-raw-source="[&lt;strong&gt;ExAllocatePoolWithTagPriority&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544523)"> <strong>ExAllocatePoolWithTagPriority</strong> </a> IRQL でその実行はときにのみ&lt;= DISPATCH_LEVEL します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqlexapclte1.md" data-raw-source="[&lt;strong&gt;IrqlExApcLte1&lt;/strong&gt;](wdm-irqlexapclte1.md)"><strong>IrqlExApcLte1</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlexapclte1.md" data-raw-source="[&lt;strong&gt;IrqlExApcLte1&lt;/strong&gt;](wdm-irqlexapclte1.md)"> <strong>IrqlExApcLte1</strong> </a>ルールでは、ドライバーを呼び出すことを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff544337" data-raw-source="[&lt;strong&gt;ExAcquireFastMutex&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544337)"> <strong>ExAcquireFastMutex</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff545647" data-raw-source="[&lt;strong&gt;ExTryToAcquireFastMutex&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545647)"> <strong>ExTryToAcquireFastMutex</strong> </a> IRQL でのみ&lt;APC_LEVEL を = です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlexapclte2.md" data-raw-source="[&lt;strong&gt;IrqlExApcLte2&lt;/strong&gt;](wdm-irqlexapclte2.md)"><strong>IrqlExApcLte2</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlexapclte2.md" data-raw-source="[&lt;strong&gt;IrqlExApcLte2&lt;/strong&gt;](wdm-irqlexapclte2.md)"> <strong>IrqlExApcLte2</strong> </a>ルールでは、IRQL でのみ、ドライバーが、次のルーチンを呼び出すことを指定します&lt;APC_LEVEL を = です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqlexapclte3.md" data-raw-source="[&lt;strong&gt;IrqlExApcLte3&lt;/strong&gt;](wdm-irqlexapclte3.md)"><strong>IrqlExApcLte3</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlexapclte3.md" data-raw-source="[&lt;strong&gt;IrqlExApcLte3&lt;/strong&gt;](wdm-irqlexapclte3.md)"> <strong>IrqlExApcLte3</strong> </a>ルールでは、ドライバーが IRQL でのみ、次のエグゼクティブ サポート ルーチンを呼び出すことを指定します&lt;APC_LEVEL を = です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlexapclteinline.md" data-raw-source="[&lt;strong&gt;IrqlExApcLteInline&lt;/strong&gt;](wdm-irqlexapclteinline.md)"><strong>IrqlExApcLteInline</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlexapclteinline.md" data-raw-source="[&lt;strong&gt;IrqlExApcLteInline&lt;/strong&gt;](wdm-irqlexapclteinline.md)"> <strong>IrqlExApcLteInline</strong> </a>ルールでは、Ddi が適切な IRQL レベルでのみ呼び出されることを指定します</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqlexfree1.md" data-raw-source="[&lt;strong&gt;IrqlExFree1&lt;/strong&gt;](wdm-irqlexfree1.md)"><strong>IrqlExFree1</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlexfree1.md" data-raw-source="[&lt;strong&gt;IrqlExFree1&lt;/strong&gt;](wdm-irqlexfree1.md)"> <strong>IrqlExFree1</strong> </a>ルールを指定する<a href="https://msdn.microsoft.com/library/windows/hardware/ff544590" data-raw-source="[&lt;strong&gt;ExFreePool&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544590)"> <strong>ExFreePool</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff544593" data-raw-source="[&lt;strong&gt;ExFreePoolWithTag&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544593)"> <strong>ExFreePoolWithTag</strong></a>は適切な IRQL で呼び出されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlexfree2.md" data-raw-source="[&lt;strong&gt;IrqlExFree2&lt;/strong&gt;](wdm-irqlexfree2.md)"><strong>IrqlExFree2</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlexfree2.md" data-raw-source="[&lt;strong&gt;IrqlExFree2&lt;/strong&gt;](wdm-irqlexfree2.md)"> <strong>IrqlExFree2</strong> </a>ルールを指定する<a href="https://msdn.microsoft.com/library/windows/hardware/ff544590" data-raw-source="[&lt;strong&gt;ExFreePool&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544590)"> <strong>ExFreePool</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff544593" data-raw-source="[&lt;strong&gt;ExFreePoolWithTag&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544593)"> <strong>ExFreePoolWithTag</strong></a>は適切な IRQL で呼び出されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqlexfree3.md" data-raw-source="[&lt;strong&gt;IrqlExFree3&lt;/strong&gt;](wdm-irqlexfree3.md)"><strong>IrqlExFree3</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlexfree3.md" data-raw-source="[&lt;strong&gt;IrqlExFree3&lt;/strong&gt;](wdm-irqlexfree3.md)"> <strong>IrqlExFree3</strong> </a>ルールを指定する<a href="https://msdn.microsoft.com/library/windows/hardware/ff544590" data-raw-source="[&lt;strong&gt;ExFreePool&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544590)"> <strong>ExFreePool</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff544593" data-raw-source="[&lt;strong&gt;ExFreePoolWithTag&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544593)"> <strong>ExFreePoolWithTag</strong></a>は適切な IRQL で呼び出されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlexpassive.md" data-raw-source="[&lt;strong&gt;IrqlExPassive&lt;/strong&gt;](wdm-irqlexpassive.md)"><strong>IrqlExPassive</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlexpassive.md" data-raw-source="[&lt;strong&gt;IrqlExPassive&lt;/strong&gt;](wdm-irqlexpassive.md)"> <strong>IrqlExPassive</strong> </a>ルールでは、ドライバーが IRQL でのみ、次のエグゼクティブ サポート ルーチンを呼び出すことを指定します PASSIVE_LEVEL を =。</p>
<ul>
<li><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff544560" data-raw-source="[&lt;strong&gt;ExCreateCallback&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544560)"><strong>ExCreateCallback</strong></a></p></li>
<li><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff545442" data-raw-source="[&lt;strong&gt;ExIsProcessorFeaturePresent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545442)"><strong>ExIsProcessorFeaturePresent</strong></a></p></li>
<li><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff545509" data-raw-source="[&lt;strong&gt;ExRaiseAccessViolation&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545509)"><strong>ExRaiseAccessViolation</strong></a></p></li>
<li><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff545524" data-raw-source="[&lt;strong&gt;ExRaiseDatatypeMisalignment&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545524)"><strong>ExRaiseDatatypeMisalignment</strong></a></p></li>
<li><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff545529" data-raw-source="[&lt;strong&gt;ExRaiseStatus&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545529)"><strong>ExRaiseStatus</strong></a></p></li>
<li><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff545658" data-raw-source="[&lt;strong&gt;ExUuidCreate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545658)"><strong>ExUuidCreate</strong></a></p></li>
</ul>
<p><a href="wdm-irqlexpassive.md" data-raw-source="[&lt;strong&gt;IrqlExPassive&lt;/strong&gt;](wdm-irqlexpassive.md)"> <strong>IrqlExPassive</strong> </a>もルールでは、ドライバーを呼び出すことを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff545529" data-raw-source="[&lt;strong&gt;ExRaiseStatus&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545529)"> <strong>ExRaiseStatus</strong> </a> IRQL で&lt;APC_LEVEL を =</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqlioapclte.md" data-raw-source="[&lt;strong&gt;IrqlIoApcLte&lt;/strong&gt;](wdm-irqlioapclte.md)"><strong>IrqlIoApcLte</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlioapclte.md" data-raw-source="[&lt;strong&gt;IrqlIoApcLte&lt;/strong&gt;](wdm-irqlioapclte.md)"> <strong>IrqlIoApcLte</strong> </a>ルールでは、IRQL で実行されている場合にのみ、ドライバーが、次の I/O マネージャー ルーチンを呼び出すことを指定します&lt;APC_LEVEL を =。</p>
<ul>
<li><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549083" data-raw-source="[&lt;strong&gt;IoDeleteDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549083)"><strong>IoDeleteDevice</strong></a></p></li>
<li><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549247" data-raw-source="[&lt;strong&gt;IoGetInitialStack&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549247)"><strong>IoGetInitialStack</strong></a></p></li>
<li><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549482" data-raw-source="[&lt;strong&gt;IoRaiseHardError&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549482)"><strong>IoRaiseHardError</strong></a></p></li>
<li><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549488" data-raw-source="[&lt;strong&gt;IoRaiseInformationalHardError&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549488)"><strong>IoRaiseInformationalHardError</strong></a></p></li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqliodispatch.md" data-raw-source="[&lt;strong&gt;IrqlIoDispatch&lt;/strong&gt;](wdm-irqliodispatch.md)"><strong>IrqlIoDispatch</strong></a></p></td>
<td align="left"><p><a href="wdm-irqliodispatch.md" data-raw-source="[&lt;strong&gt;IrqlIoDispatch&lt;/strong&gt;](wdm-irqliodispatch.md)"> <strong>IrqlIoDispatch</strong> </a>ルールでは、IRQL で実行されている場合にのみ、ドライバーが、次の I/O マネージャー ルーチンを呼び出すことを指定します&lt;= DISPATCH_LEVEL:<a href="https://msdn.microsoft.com/library/windows/hardware/ff549212" data-raw-source="[&lt;strong&gt;IoGetDeviceToVerify&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549212)"><strong>IoGetDeviceToVerify</strong></a>、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff548529" data-raw-source="[&lt;strong&gt;IoSetDeviceToVerify&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548529)"> <strong>IoSetDeviceToVerify</strong></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqliopassive1.md" data-raw-source="[&lt;strong&gt;IrqlIoPassive1&lt;/strong&gt;](wdm-irqliopassive1.md)"><strong>IrqlIoPassive1</strong></a></p></td>
<td align="left"><p><a href="wdm-irqliopassive1.md" data-raw-source="[&lt;strong&gt;IrqlIoPassive1&lt;/strong&gt;](wdm-irqliopassive1.md)"> <strong>IrqlIoPassive1</strong> </a>ルールでは、IRQL で実行されている場合にのみ、ドライバーが、次のルーチンを呼び出すことを指定します PASSIVE_LEVEL を =。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqliopassive2.md" data-raw-source="[&lt;strong&gt;IrqlIoPassive2&lt;/strong&gt;](wdm-irqliopassive2.md)"><strong>IrqlIoPassive2</strong></a></p></td>
<td align="left"><p><a href="wdm-irqliopassive2.md" data-raw-source="[&lt;strong&gt;IrqlIoPassive2&lt;/strong&gt;](wdm-irqliopassive2.md)"> <strong>IrqlIoPassive2</strong> </a>ルールでは、ドライバーが IRQL でのみ、次の I/O マネージャー ルーチンを呼び出すことを指定します PASSIVE_LEVEL を =。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqliopassive3.md" data-raw-source="[&lt;strong&gt;IrqlIoPassive3&lt;/strong&gt;](wdm-irqliopassive3.md)"><strong>IrqlIoPassive3</strong></a></p></td>
<td align="left"><p>IrqlIoPassive3 ルールでは、IRQL で実行されている場合にのみ、ドライバーが、次のルーチンを呼び出すことを指定します PASSIVE_LEVEL を =。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqliopassive4.md" data-raw-source="[&lt;strong&gt;IrqlIoPassive4&lt;/strong&gt;](wdm-irqliopassive4.md)"><strong>IrqlIoPassive4</strong></a></p></td>
<td align="left"><p><a href="wdm-irqliopassive4.md" data-raw-source="[&lt;strong&gt;IrqlIoPassive4&lt;/strong&gt;](wdm-irqliopassive4.md)"> <strong>IrqlIoPassive4</strong> </a>ルールでは、IRQL で実行されている場合にのみ、ドライバーが、次のルーチンを呼び出すことを指定します PASSIVE_LEVEL を =。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqliopassive5.md" data-raw-source="[&lt;strong&gt;IrqlIoPassive5&lt;/strong&gt;](wdm-irqliopassive5.md)"><strong>IrqlIoPassive5</strong></a></p></td>
<td align="left"><p><a href="wdm-irqliopassive5.md" data-raw-source="[&lt;strong&gt;IrqlIoPassive5&lt;/strong&gt;](wdm-irqliopassive5.md)"> <strong>IrqlIoPassive5</strong> </a>ルールでは、IRQL で実行されている場合にのみ、ドライバーが特定の I/O マネージャー ルーチンを呼び出すことを指定します PASSIVE_LEVEL を = です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlkeapclte1.md" data-raw-source="[&lt;strong&gt;IrqlKeApcLte1&lt;/strong&gt;](wdm-irqlkeapclte1.md)"><strong>IrqlKeApcLte1</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlkeapclte1.md" data-raw-source="[&lt;strong&gt;IrqlKeApcLte1&lt;/strong&gt;](wdm-irqlkeapclte1.md)"> <strong>IrqlKeApcLte1</strong> </a>ルールでは、IRQL で実行されている場合にのみ、ドライバーが、次のカーネル ルーチンを呼び出すことを指定します&lt;APC_LEVEL を =。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqlkeapclte2.md" data-raw-source="[&lt;strong&gt;IrqlKeApcLte2&lt;/strong&gt;](wdm-irqlkeapclte2.md)"><strong>IrqlKeApcLte2</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlkeapclte2.md" data-raw-source="[&lt;strong&gt;IrqlKeApcLte2&lt;/strong&gt;](wdm-irqlkeapclte2.md)"> <strong>IrqlKeApcLte2</strong> </a>ルールでは、IRQL で実行されている場合にのみ、ドライバーが、次のカーネル ルーチンを呼び出すことを指定します&lt;APC_LEVEL を =。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlkedispatchlte.md" data-raw-source="[&lt;strong&gt;IrqlKeDispatchLte&lt;/strong&gt;](wdm-irqlkedispatchlte.md)"><strong>IrqlKeDispatchLte</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlkedispatchlte.md" data-raw-source="[&lt;strong&gt;IrqlKeDispatchLte&lt;/strong&gt;](wdm-irqlkedispatchlte.md)"> <strong>IrqlKeDispatchLte</strong> </a>ルールでは、IRQL で実行されている場合にのみ、ドライバーが、次のカーネル ルーチンを呼び出すことを指定します&lt;= DISPATCH_LEVEL:</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqlkeraiselower.md" data-raw-source="[&lt;strong&gt;IrqlKeRaiseLower&lt;/strong&gt;](wdm-irqlkeraiselower.md)"><strong>IrqlKeRaiseLower</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff547817" data-raw-source="[&lt;strong&gt;IrqlKeRaiseLower&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547817)"> <strong>IrqlKeRaiseLower</strong> </a>ルールでは、ドライバーは、IRQL 値の増減すると、次でことを指定します。</p>
ドライバーを呼び出すと<a href="https://msdn.microsoft.com/library/windows/hardware/ff553079" data-raw-source="[&lt;strong&gt;KeRaiseIrql&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553079)"> <strong>KeRaiseIrql</strong></a>よりも小さい IRQL で実行されているかの値と等しく、 <em>NewIrql</em>パラメーター。<br />
ドライバー呼び出し<a href="https://msdn.microsoft.com/library/windows/hardware/ff552968" data-raw-source="[&lt;strong&gt;KeLowerIrql&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552968)"> <strong>KeLowerIrql</strong> </a>呼び出した後のみ<strong>KeRaiseIrql</strong>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff553084" data-raw-source="[&lt;strong&gt;KeRaiseIrqlToDpcLevel&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553084)"> <strong>KeRaiseIrqlToDpcLevel</strong> </a>.<br />
</td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlkeraiselower2.md" data-raw-source="[&lt;strong&gt;IrqlKeRaiseLower2&lt;/strong&gt;](wdm-irqlkeraiselower2.md)"><strong>IrqlKeRaiseLower2</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlkeraiselower2.md" data-raw-source="[&lt;strong&gt;IrqlKeRaiseLower2&lt;/strong&gt;](wdm-irqlkeraiselower2.md)"> <strong>IrqlKeRaiseLower2</strong> </a>ルールでは、ドライバーが使用することを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff552968" data-raw-source="[&lt;strong&gt;KeLowerIrql&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552968)"> <strong>KeLowerIrql</strong> </a>前の呼び出しによって発生した元の IRQL を復元するには<a href="https://msdn.microsoft.com/library/windows/hardware/ff553079" data-raw-source="[&lt;strong&gt;KeRaiseIrql&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553079)"> <strong>KeRaiseIrql</strong> </a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff553084" data-raw-source="[&lt;strong&gt;KeRaiseIrqlToDpcLevel&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553084)"> <strong>KeRaiseIrqlToDpcLevel</strong></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqlkereleasespinlock.md" data-raw-source="[&lt;strong&gt;IrqlKeReleaseSpinLock&lt;/strong&gt;](wdm-irqlkereleasespinlock.md)"><strong>IrqlKeReleaseSpinLock</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlkereleasespinlock.md" data-raw-source="[&lt;strong&gt;IrqlKeReleaseSpinLock&lt;/strong&gt;](wdm-irqlkereleasespinlock.md)"> <strong>IrqlKeReleaseSpinLock</strong> </a>ルールでは、ドライバーを呼び出すことを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff553145" data-raw-source="[&lt;strong&gt;KeReleaseSpinLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553145)"> <strong>KeReleaseSpinLock</strong> </a>のみときに実行されている IRQL で =DISPATCH_LEVEL します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlkesetevent.md" data-raw-source="[&lt;strong&gt;IrqlKeSetEvent&lt;/strong&gt;](wdm-irqlkesetevent.md)"><strong>IrqlKeSetEvent</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlkesetevent.md" data-raw-source="[&lt;strong&gt;IrqlKeSetEvent&lt;/strong&gt;](wdm-irqlkesetevent.md)"> <strong>IrqlKeSetEvent</strong> </a>ルールでは、ことを指定します、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff553253" data-raw-source="[&lt;strong&gt;KeSetEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553253)"> <strong>KeSetEvent</strong> </a>ルーチンは IRQL でのみ呼び出す&lt;= DISPATCH_LEVELときに<em>待機</em>に設定されている<strong>FALSE</strong>、IRQL で&lt;APC_LEVEL = とき<em>待機</em>に設定されている<strong>TRUE</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqlkewaitformutexobject.md" data-raw-source="[&lt;strong&gt;IrqlKeWaitForMutexObject&lt;/strong&gt;](wdm-irqlkewaitformutexobject.md)"><strong>IrqlKeWaitForMutexObject</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlkewaitformutexobject.md" data-raw-source="[&lt;strong&gt;IrqlKeWaitForMutexObject&lt;/strong&gt;](wdm-irqlkewaitformutexobject.md)"> <strong>IrqlKeWaitForMutexObject</strong> </a>ルールを呼び出すドライバーを指定します、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff553344" data-raw-source="[&lt;strong&gt;KeWaitForMutexObject&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553344)"> <strong>KeWaitForMutexObject</strong> </a>適切な IRQL で日常的な値に基づいて、<em>タイムアウト</em>パラメーター。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlkewaitformultipleobjects.md" data-raw-source="[&lt;strong&gt;IrqlKeWaitForMultipleObjects&lt;/strong&gt;](wdm-irqlkewaitformultipleobjects.md)"><strong>IrqlKeWaitForMultipleObjects</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlkewaitformultipleobjects.md" data-raw-source="[&lt;strong&gt;IrqlKeWaitForMultipleObjects&lt;/strong&gt;](wdm-irqlkewaitformultipleobjects.md)"> <strong>IrqlKeWaitForMultipleObjects</strong> </a>ことを指定するルールの呼び出し元、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff553324" data-raw-source="[&lt;strong&gt;KeWaitForMultipleObjects&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553324)"> <strong>KeWaitForMultipleObjects</strong> </a>ルーチンを実行する必要があります基に適切な IRQL で、<em>タイムアウト</em>パラメーター。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqlmmapclte.md" data-raw-source="[&lt;strong&gt;IrqlMmApcLte&lt;/strong&gt;](wdm-irqlmmapclte.md)"><strong>IrqlMmApcLte</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlmmapclte.md" data-raw-source="[&lt;strong&gt;IrqlMmApcLte&lt;/strong&gt;](wdm-irqlmmapclte.md)"> <strong>IrqlMmApcLte</strong> </a>ルールを指定するドライバー ルーチンを呼び出して次のメモリ マネージャー IRQL で実行されている場合にのみ&lt;APC_LEVEL を =。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlmmdispatch.md" data-raw-source="[&lt;strong&gt;IrqlMmDispatch&lt;/strong&gt;](wdm-irqlmmdispatch.md)"><strong>IrqlMmDispatch</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlmmdispatch.md" data-raw-source="[&lt;strong&gt;IrqlMmDispatch&lt;/strong&gt;](wdm-irqlmmdispatch.md)"> <strong>IrqlMmDispatch</strong> </a>ルールでは、ドライバーを呼び出すことを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff554503" data-raw-source="[&lt;strong&gt;MmFreeContiguousMemory&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554503)"> <strong>MmFreeContiguousMemory</strong> </a>のみとことで実行されている<strong>IRQL &lt;= DISPATCH_LEVEL</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqlobpassive.md" data-raw-source="[&lt;strong&gt;IrqlObPassive&lt;/strong&gt;](wdm-irqlobpassive.md)"><strong>IrqlObPassive</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlobpassive.md" data-raw-source="[&lt;strong&gt;IrqlObPassive&lt;/strong&gt;](wdm-irqlobpassive.md)"> <strong>IrqlObPassive</strong> </a>ルールでは、ドライバーを呼び出すことを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff558679" data-raw-source="[&lt;strong&gt;ObReferenceObjectByHandle&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff558679)"> <strong>ObReferenceObjectByHandle</strong> </a>のみときに実行されている IRQL で =PASSIVE_LEVEL します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlpspassive.md" data-raw-source="[&lt;strong&gt;IrqlPsPassive&lt;/strong&gt;](wdm-irqlpspassive.md)"><strong>IrqlPsPassive</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlpspassive.md" data-raw-source="[&lt;strong&gt;IrqlPsPassive&lt;/strong&gt;](wdm-irqlpspassive.md)"> <strong>IrqlPsPassive</strong> </a>ルールでは、ドライバーが、次を呼び出すことを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff559917" data-raw-source="[&lt;strong&gt;Process Structure routines&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559917)"><strong>構造の処理ルーチン</strong></a>のみ実行するに場合IRQL で PASSIVE_LEVEL を = します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqlreturn.md" data-raw-source="[&lt;strong&gt;IrqlReturn&lt;/strong&gt;](wdm-irqlreturn.md)"><strong>IrqlReturn</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlreturn.md" data-raw-source="[&lt;strong&gt;IrqlReturn&lt;/strong&gt;](wdm-irqlreturn.md)"> <strong>IrqlReturn</strong> </a>ルールでは、ドライバーのディスパッチ ルーチンが呼び出される位置同じ IRQL で返すことを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlrtlpassive.md" data-raw-source="[&lt;strong&gt;IrqlRtlPassive&lt;/strong&gt;](wdm-irqlrtlpassive.md)"><strong>IrqlRtlPassive</strong></a></p></td>
<td align="left"><p>IrqlRtlPassive ルールでは、ドライバーを呼び出すことを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff561829" data-raw-source="[&lt;strong&gt;RtlDeleteRegistryValue&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561829)"> <strong>RtlDeleteRegistryValue</strong> </a> IRQL でその実行はときにのみ PASSIVE_LEVEL を = です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqlzwpassive.md" data-raw-source="[&lt;strong&gt;IrqlZwPassive&lt;/strong&gt;](wdm-irqlzwpassive.md)"><strong>IrqlZwPassive</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlzwpassive.md" data-raw-source="[&lt;strong&gt;IrqlZwPassive&lt;/strong&gt;](wdm-irqlzwpassive.md)"> <strong>IrqlZwPassive</strong> </a>ルールでは、ドライバーを呼び出すことを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff566417" data-raw-source="[&lt;strong&gt;ZwClose&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566417)"> <strong>ZwClose</strong> </a> IRQL でその実行はときにのみ PASSIVE_LEVEL を = です。</p></td>
</tr>
</tbody>
</table>

 

**Irql ルールを選択するには、次のように設定します。**

1.  Microsoft Visual Studio で、ドライバーのプロジェクト (.vcxProj) を選択します。 **ドライバー**  メニューのをクリックして**Static Driver Verifier を起動しています**.

2.  をクリックして、**ルール**タブ。**規則セット**、 **Irql**します。

    Visual Studio の開発者コマンド プロンプト ウィンドウから既定のルールを選択するには、次のように指定します。 **Irql.sdv**で、 **/check**オプション。 以下に例を示します。

    ```
    msbuild /t:sdv /p:Inputs="/check:Irql.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    詳細については、次を参照してください。[ドライバーで障害を検出する Static Driver Verifier を使用して](https://msdn.microsoft.com/library/windows/hardware/hh454281)と[Static Driver Verifier のコマンド (MSBuild)](https://msdn.microsoft.com/library/windows/hardware/hh466459)します。

 

 





