---
title: wdfkd.wdfpoolusage
description: Wdfkd.wdfpoolusage 拡張機能では、ドライバーのカーネル モード ドライバー フレームワーク (KMDF) の検証が有効になっている場合、指定したドライバーのプールの使用状況情報が表示されます。
ms.assetid: 6a77b76b-c970-447c-a8dd-e1ceb7add611
keywords:
- デバッグ wdfkd.wdfpoolusage Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfpoolusage
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a8c550d6c850fdfcc1acca8a46e0f409ccb038b1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536344"
---
# <a name="wdfkdwdfpoolusage"></a>!wdfkd.wdfpoolusage


**! Wdfkd.wdfpoolusage**拡張機能は、ドライバーのカーネル モード ドライバー フレームワーク (KMDF) の検証が有効になっている場合に指定したドライバーのプールの使用状況情報を表示します。

```dbgcmd
!wdfkd.wdfpoolusage [DriverName [SearchAddress] [Flags]]]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______DriverName______"></span><span id="_______drivername______"></span><span id="_______DRIVERNAME______"></span> *ドライバー名*   
(省略可能)。 ドライバーの名前。 *DriverName* .sys ファイル名拡張子を含めることはできません。

<span id="_______SearchAddress______"></span><span id="_______searchaddress______"></span><span id="_______SEARCHADDRESS______"></span> *SearchAddress*   
(省略可能)。 メモリ アドレスを表す文字列。 含むプール エントリ*SearchAddress*が表示されます。 場合*SearchAddress*が 0 または省略すると、すべてのドライバーのプールのエントリが表示されます。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
(省略可能)。 表示する情報の種類。 このパラメーターは有効な場合にのみ*SearchAddress*が 0 以外。 *フラグ*次のビットの組み合わせにすることができます。 既定値は、「0x0」です。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>ビット 0 (0x1)  
詳細な出力が表示されます。 複数の行がそれぞれ表示されます。 このフラグが設定されていない場合は、1 つの行に割り当てに関する情報が表示されます。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>ビット 1 (0x2)  
内部の表示では、ハンドルの情報を入力します。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>ビット 2 (0x4)  
プールの各エントリの呼び出し元が表示されます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>フレームワーク

KMDF 1、UMDF 2

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、次を参照してください。[カーネル モード ドライバー フレームワークのデバッグ](kernel-mode-driver-framework-debugging.md)します。

<a name="remarks"></a>注釈
-------

省略した場合、 *DriverName*パラメーター、既定のドライバーを使用します。 使用して、既定のドライバーを表示することができます、 [ **! wdfkd.wdfgetdriver** ](-wdfkd-wdfgetdriver.md) ; 拡張機能を使用して、既定のドライバーを設定することができます、 [ **! wdfkd.wdfsetdriver**](-wdfkd-wdfsetdriver.md)拡張機能。

次の例からの出力を示しています、 **! wdfpoolusage**プールの割り当てが設定されていないときに、拡張機能と*フラグ*値が 0 に設定します。

```dbgcmd
## kd> !wdfpoolusage wdfrawbusenumtest 0 0 
-----------------------------------
## FxDriverGlobals 83b7af18 pool stats
-----------------------------------
Driver Tag: 'RawB'
15126 NonPaged Bytes, 548 Paged Bytes
94 NonPaged Allocations, 10 Paged Allocations
15610 PeakNonPaged Bytes, 752 PeakPaged Bytes
100 PeakNonPaged Allocations, 14 PeakPaged Allocations

pool 82dbae00, Size  512 Tag 'RawB', NonPaged, Caller:  Wdf01000!FxVerifierLock::AllocateThreadTable+5d
```

次の例からの出力を示します **! wdfpoolusage**場合に表示される値の*フラグ*は 1。 (2 行目で省略記号 (...) を前の例に示すのと同じである何らかの出力の省略を示すことに注意してください)。

```dbgcmd
kd> !wdfpoolusage wdfrawbusenumtest 0 1 
. . . 
100 PeakNonPaged Allocations, 14 PeakPaged Allocations

Client alloc starts at 82dbae00
Size  512 Tag 'RawB'
NonPaged (0x0)
Caller:  Wdf01000!FxVerifierLock::AllocateThreadTable+5d
```

 

 





