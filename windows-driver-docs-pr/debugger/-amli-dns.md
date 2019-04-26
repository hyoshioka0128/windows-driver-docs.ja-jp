---
title: amli dns
description: Amli dns 拡張機能は、ACPI 名前空間オブジェクトを表示します。
ms.assetid: 7db937ba-109f-4f4e-8dd3-4aa5d0dc13b2
keywords:
- Windows デバッグ amli dns
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- amli dns
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1d05bafcb96bdd57130ee9d849edfebcea5d5ab3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334763"
---
# <a name="amli-dns"></a>!amli dns


**! Amli dns**拡張機能は、ACPI 名前空間オブジェクトを表示します。

構文

```dbgcmd
    !amli dns [/s] [Name | Address]
```

## <a name="span-idddkamlidnsdbgspanspan-idddkamlidnsdbgspanparameters"></a><span id="ddk__amli_dns_dbg"></span><span id="DDK__AMLI_DNS_DBG"></span>パラメーター


<span id="________s______"></span><span id="________S______"></span> **/s**   
表示されている再帰的に指定したオブジェクトの下の名前空間の全体のサブツリーをによりします。

<span id="_______Name______"></span><span id="_______name______"></span><span id="_______NAME______"></span> *名*   
名前空間のパスを指定します。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
名前空間ノードのアドレスを指定します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

関連するコマンドとその用途については、次を参照してください。 [AMLI デバッガー](the-amli-debugger.md)します。

<a name="remarks"></a>注釈
-------

どちらの場合*名前*も*アドレス*ACPI 名前空間ツリー全体が表示されている再帰的に指定します。 **/S**が指定されていない場合でも、パラメーターはこの場合と想定常にします。

このコマンドは、確認するどのような特定の名前空間オブジェクトは、メソッド、フィールド単位、デバイス、または別の種類のオブジェクト。

なし、 **/s**パラメーターでは、この拡張機能は等しく、 [ **! nsobj** ](-nsobj.md)拡張機能。 **/S**パラメーターと同じですが、 [ **! nstree** ](-nstree.md)拡張機能。

例をいくつか紹介します。 次のコマンドは、オブジェクトの名前空間を表示**bios**:

```console
AMLI(? for help)-> dns \bios

ACPI Name Space: \BIOS (80E5F378)
OpRegion(BIOS:RegionSpace=SystemMemory,Offset=0xfcb07500,Len=2816)
```

次のコマンドは、オブジェクトの名前空間を表示\_BST、およびツリーの下位に。

```console
kd> !amli dns /s \_sb.pci0.isa.bat1._bst

ACPI Name Space: \_SB.PCI0.ISA.BAT1._BST (c29c2044)
Method(_BST:Flags=0x0,CodeBuff=c29c20a5,Len=103)
```

BAT1 デバイスの名前空間を表示するには、次のように入力します。

```console
kd> !amli dns /s \_sb.pci0.isa.bat1
```

下位ドッキング ステーション デバイスにあるすべての名前空間を表示するには、次のように入力します。

```console
kd> !amli dns /s \_sb.pci0.dock
```

下位の名前空間を表示する、 \_DCK メソッド、型。

```console
kd> !amli dns /s \_sb.pci0.dock._dck
```

名前空間の全体を表示するには、次のように入力します。

```console
kd> !amli dns
```

 

 





