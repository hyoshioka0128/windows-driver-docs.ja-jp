---
title: 割り込みアフィニティ
description: 割り込みアフィニティ
ms.assetid: e36a52d0-3a94-4017-b4a1-0b41f737523c
keywords:
- 割り込みサービス ルーチン WDK カーネルのアフィニティ
- Isr WDK カーネルでは、アフィニティ
- アフィニティ ポリシー WDK の割り込み
- IRQ_DEVICE_POLICY
- プロセッサ アフィニティ WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: db9bf41015d10da67a46ae7c2e7c3f81bf731011
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539586"
---
# <a name="interrupt-affinity"></a>割り込みアフィニティ


*アフィニティ*の割り込みは、割り込みを処理できるプロセッサのセット。 各デバイスには、*アフィニティ ポリシー*します。 オペレーティング システムでは、アフィニティのポリシーを使用して、そのデバイスの割り込みのアフィニティを計算します。 アフィニティのポリシーは、デバイスの INF ファイルやレジストリ設定で指定できます。

Windows Vista 以降、管理者は、割り込みのアフィニティ ポリシーを設定するのにレジストリを使用できます。

管理者は、下にある次のエントリを設定できます、 **\\管理の割り込み\\アフィニティ ポリシー**レジストリ キー。

-   **DevicePolicy** 21\_アフィニティのポリシーを指定する DWORD の値。 考えられる各設定に対応する[ **IRQ\_デバイス\_ポリシー** ](https://msdn.microsoft.com/library/windows/hardware/ff551783)値。


-   **AssignmentSetOverride** 21\_バイナリ値を指定する、 [ **KAFFINITY** ](#about-kaffinity)マスク。 場合**DevicePolicy** 0x04 です (**IrqPolicySpecifiedProcessors**)、このマスクを割り当てるデバイスの割り込みをプロセッサのセットを指定します。

次の表、 [ **IRQ\_デバイス\_ポリシー** ](https://msdn.microsoft.com/library/windows/hardware/ff551783)値、および対応するレジストリの設定**DevicePolicy**します。 各値の意味の詳細については、[ **IRQ\_デバイス\_ポリシー**](https://msdn.microsoft.com/library/windows/hardware/ff551783)を参照してください。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>IRQ_DEVICE_POLICY 値</th>
<th>レジストリ内の数値の値</th>
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

 

ドライバーの INF ファイルには、レジストリ値の既定の設定を指定できます。 設定する方法の例を次に示します、 **DevicePolicy**値を**IrqPolicyOneCloseProcessor** INF ファイルにします。 詳細については、[ **INF AddReg ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546320)を参照してください。

```cpp
[install-section-name.HW]
AddReg=add-registry-section 

[add-registry-section]
HKR, "Interrupt Management\Affinity Policy", DevicePolicy, 0x00010001, 2
```

システム レジストリ設定を使用できるように、デバイスのドライバーを送信するとき、 [ **IRP\_MN\_フィルター\_リソース\_要件**](https://msdn.microsoft.com/library/windows/hardware/ff550874)IRP がドライバーにします。 オペレーティング システムが提供、 [ **IO\_リソース\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff550598)で各割り込みの構造、**型**メンバーに設定**CmResourceTypeInterrupt**します。 メッセージ シグナル割り込みなど、CM の\_リソース\_割り込み\_のビットのメッセージ、**フラグ**メンバーの設定は明確では、それ以外の場合。 **U.Interrupt**メンバーは、割り込みの設定を示します。

次の表は、レジストリ設定とメンバーの間の通信**u.Interrupt**します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>レジストリ値</th>
<th>You.Interrupt のメンバー</th>
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

KAFFINITY 型は、グループ内の論理プロセッサのセットを表す関係マスクです。

```cpp
typedef ULONG_PTR  KAFFINITY;
```

KAFFINITY 型では、32 ビット バージョンの Windows で 32 ビットし、64 ビット Windows の 64 ビット バージョンでは。

グループに n 個の論理プロセッサが含まれている場合、プロセッサは、n-1 する、0 から番号が。 グループ内のプロセッサ番号 i は、i が 0 n-1 の範囲内にある、関係マスクのビット i で表されます。 論理プロセッサに対応していないアフィニティ マスクのビットは常に 0 です。

たとえば、KAFFINITY 値は、グループ内のアクティブなプロセッサを識別する場合、プロセッサ マスクのビットは 1 つ場合は、プロセッサがアクティブになり、プロセッサがアクティブでない場合は 0。

関係マスクのビット数は、グループ内の論理プロセッサの最大数を決定します。 Windows の 64 ビット バージョンでは、グループごとのプロセッサの最大数には 64 です。 Windows の 32 ビット バージョンでは、グループごとのプロセッサの最大数には 32 です。 呼び出す、 [ **KeQueryMaximumProcessorCountEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-kequerymaximumprocessorcountex)ルーチンをグループごとのプロセッサの最大数を取得します。 この数は、マルチプロセッサ システムのハードウェア構成によって異なりますが、それぞれ、Windows の 64 ビットおよび 32 ビット バージョンで設定されている固定の 64 プロセッサと 32 プロセッサ制限を超えることはありません。

[ **GROUP_AFFINITY** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/miniport/ns-miniport-_group_affinity)構造には、affinity mask オプションとグループの番号が含まれています。 グループ番号では、関係マスクを適用するグループを識別します。

カーネル ルーチン KAFFINITY 型を使用するには、 [ **IoConnectInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioconnectinterrupt)、 [ **KeQueryActiveProcessorCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-kequeryactiveprocessorcount)、および[**KeQueryActiveProcessors**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-kequeryactiveprocessors)します。 

 

 

 




