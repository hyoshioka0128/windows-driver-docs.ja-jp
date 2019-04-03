---
title: wdfkd.wdfinterrupt
description: Wdfkd.wdfinterrupt 拡張機能では、WDFINTERRUPT オブジェクトに関する情報が表示されます。
ms.assetid: 3e032095-94fe-41d5-aeed-645d6b544105
keywords:
- デバッグ wdfkd.wdfinterrupt Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfinterrupt
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 58158aead119ad37bf6eca40e4c1fabbda2e7070
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528842"
---
# <a name="wdfkdwdfinterrupt"></a>!wdfkd.wdfinterrupt


**! Wdfkd.wdfinterrupt**拡張機能が WDFINTERRUPT オブジェクトに関する情報を表示します。

```dbgcmd
!wdfkd.wdfinterrupt Handle [Flags]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span> *ハンドル*   
WDFINTERRUPT オブジェクトへのハンドル。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
(省略可能)。 表示する情報の種類を指定します。 *フラグ*次のビットの組み合わせにすることができます。 既定値は、「0x0」です。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>ビット 0 (0x1)  
この WDFINTERRUPT オブジェクトに関連付けられた割り込みディスパッチ テーブル (IDT) の割り込みサービス ルーチン (Isr) が表示されます。 このフラグの設定に従って、 **! wdfinterrupt**拡張機能、 [ **! idt** ](-idt.md)拡張機能。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>フレームワーク

KMDF 1、UMDF 2

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、[カーネル モード ドライバー フレームワークのデバッグ](kernel-mode-driver-framework-debugging.md)を参照してください。

<a name="remarks"></a>注釈
-------

次の例の出力を示しています、 **! wdfinterrupt**ビット 0 設定を使用して拡張機能、*フラグ*パラメーター (そのため、出力には、IDT に関する情報が表示されます)。

```dbgcmd
kd> !wdfkd.wdfinterrupt 0x7a988698  1 

# Dumping WDFINTERRUPT 0x7a988698
=========================
  Interrupt Type: Line-based, Connected, Enabled
  Vector: 0xa1 (!idt 0xa1)
  Irql: 0x9
  Mode: LevelSensitive
  Polarity: WdfInterruptPolarityUnknown
  ShareDisposition: CmResourceShareShared
  FloatingSave: FALSE
  Interrupt Priority Policy: WdfIrqPriorityUndefined
  Processor Affinity Policy: WdfIrqPolicyOneCloseProcessor
  Processor Group: 0
  Processor Affinity: 0x3

  dt nt!KINTERRUPT 0x8594eb28

  EvtInterruptIsr: 1394ohci!Interrupt::WdfEvtInterruptIsr (0x8d580552)
  EvtInterruptDpc: 1394ohci!Interrupt::WdfEvtInterruptDpc (0x8d580682)

Dumping IDT:

a1:          85167a58 ndis!ndisMiniportIsr (KINTERRUPT 85167a00)
                                    Wdf01000!FxInterrupt::_InterruptThunk (KINTERRUPT 85987500)

To get ISR from KINTERRUPT: 
   dt <KINTERRUPT> nt!KINTERRUPT ServiceContext
   dt <ServiceContext> wdf01000!FxInterrupt m_EvtInterruptIsr
```

前の例では、表示の最後の 2 つの提案[ **dt (型の表示)** ](dt--display-type-.md)コマンドの追加のデータを表示するために使用できます。

 

 





