---
title: 割り込みアフィニティ
description: 割り込みアフィニティ
ms.assetid: e36a52d0-3a94-4017-b4a1-0b41f737523c
keywords:
- 割り込みサービスルーチン WDK カーネル、アフィニティ
- Isr WDK カーネル, アフィニティ
- アフィニティポリシー WDK 割り込み
- IRQ_DEVICE_POLICY
- プロセッサアフィニティ WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a329fba47eb6c5e45eb704ca20b9523e6ee239e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828288"
---
# <a name="interrupt-affinity"></a>割り込みアフィニティ


割り込みの*関係*は、割り込みを処理できるプロセッサのセットです。 各デバイスには*アフィニティポリシー*があります。 オペレーティングシステムは、アフィニティポリシーを使用して、そのデバイスの割り込みの関係を計算します。 アフィニティポリシーは、デバイスの INF ファイルまたはレジストリ設定で指定できます。

Windows Vista 以降では、管理者はレジストリを使用して、割り込みのアフィニティポリシーを設定できます。

管理者は、 **\\割り込み管理\\アフィニティポリシー**のレジストリキーの下に、次のエントリを設定できます。

-   **Devicepolicy**は、アフィニティポリシーを指定する REG\_DWORD 値です。 考えられる各設定は、 [**IRQ\_デバイス\_ポリシー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_irq_device_policy)値に対応します。


-   **AssignmentSetOverride**は、 [**kaffinity**](#about-kaffinity) MASK を指定する REG\_バイナリ値です。 **Devicepolicy**が 0X04 (**IrqPolicySpecifiedProcessors**) の場合、このマスクは、デバイスの割り込みを割り当てるプロセッサのセットを指定します。

次の表に、 [**IRQ\_デバイス\_ポリシー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_irq_device_policy)値、および**devicepolicy**の対応するレジストリ設定を示します。 各値の意味の詳細については、「 [**IRQ\_デバイス\_ポリシー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_irq_device_policy)」を参照してください。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>IRQ_DEVICE_POLICY 値</th>
<th>レジストリ内の数値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>IrqPolicyMachineDefault</strong></p></td>
<td><p>0x00</p></td>
</tr>
<tr class="even">
<td><p><strong>IrqPolicyAllCloseProcessors</strong></p></td>
<td><p>0x01</p></td>
</tr>
<tr class="odd">
<td><p><strong>IrqPolicyOneCloseProcessor</strong></p></td>
<td><p>0x02</p></td>
</tr>
<tr class="even">
<td><p><strong>IrqPolicyAllProcessorsInMachine</strong></p></td>
<td><p>0x03</p></td>
</tr>
<tr class="odd">
<td><p><strong>IrqPolicySpecifiedProcessors</strong></p></td>
<td><p>0x04</p></td>
</tr>
<tr class="even">
<td><p><strong>IrqPolicySpreadMessagesAcrossAllProcessors</strong></p></td>
<td><p>0x05</p></td>
</tr>
</tbody>
</table>

 

ドライバーの INF ファイルでは、レジストリ値の既定の設定を指定できます。 次に示すのは、ファイルの**Devicepolicy**の値を**IrqPolicyOneCloseProcessor**に設定する方法の例です。 詳細については、「 [**INF AddReg ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)」を参照してください。

```cpp
[install-section-name.HW]
AddReg=add-registry-section 

[add-registry-section]
HKR, "Interrupt Management\Affinity Policy", DevicePolicy, 0x00010001, 2
```

システムは、 [**irp\_\_フィルター\_リソース\_要件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-filter-resource-requirements)の irp をドライバーに送信するときに、そのデバイスのドライバーがレジストリ設定を使用できるようにします。 オペレーティングシステムは、**型**のメンバーが**cmresourcetypeinterrupt**に設定されている各割り込みに対して、 [**IO\_リソース\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_resource_descriptor)構造を提供します。 メッセージシグナル割り込みの場合は、CM\_リソース\_INTERRUPT\_メッセージビットの**Flags**メンバーが設定されます。それ以外の場合は、明らかになります。 この**interrupt メンバーは**、割り込みの設定を記述します。

次の表に、レジストリ設定と**u. Interrupt**のメンバーの対応を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>レジストリ値</th>
<th>あなたのメンバー。中断</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>DevicePolicy</strong></p></td>
<td><p><strong>AffinityPolicy</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>AssignmentSetOverride</strong></p></td>
<td><p><strong>TargetedProcessors</strong></p></td>
</tr>
</tbody>
</table>

## <a name="about-kaffinity"></a>KAFFINITY について

KAFFINITY の種類は、グループ内の論理プロセッサのセットを表す関係マスクです。

```cpp
typedef ULONG_PTR  KAFFINITY;
```

KAFFINITY 型は、32ビットバージョンの Windows では32ビットであり、64ビットバージョンの Windows では64ビットです。

グループに n 個の論理プロセッサが含まれている場合、プロセッサには 0 ~ n-1 の番号が付けられます。 グループのプロセッサ番号は、affinity mask のビット i で表されます。ここで、i の範囲は 0 ~ n-1 です。 論理プロセッサに対応しない関係マスクビットは常に0です。

たとえば、KAFFINITY 値がグループ内のアクティブなプロセッサを識別する場合、プロセッサのマスクビットはプロセッサがアクティブである場合は1になり、プロセッサがアクティブでない場合は0になります。

アフィニティマスクのビット数によって、グループ内の論理プロセッサの最大数が決まります。 Windows の64ビットバージョンでは、グループあたりのプロセッサの最大数は64です。 Windows の32ビットバージョンでは、グループあたりのプロセッサの最大数は32です。 [**KeQueryMaximumProcessorCountEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-kequerymaximumprocessorcountex)ルーチンを呼び出して、グループあたりのプロセッサの最大数を取得します。 この数値は、マルチプロセッサシステムのハードウェア構成によって異なりますが、それぞれ64ビットバージョンと32ビットバージョンの Windows で設定されている64プロセッサと32プロセッサの固定値を超えることはできません。

[**GROUP_AFFINITY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/miniport/ns-miniport-_group_affinity)構造体には、関係マスクとグループ番号が含まれています。 グループ番号は、関係マスクが適用されるグループを識別します。

KAFFINITY の種類を使用するカーネルルーチンには、 [**Ioconnectinterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterrupt)、 [**kequeryactiveprocessorcount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-kequeryactiveprocessorcount)、 [**kequeryactiveprocessor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-kequeryactiveprocessors)などがあります。 

 

 

 




