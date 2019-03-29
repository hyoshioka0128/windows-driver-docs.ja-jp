---
title: isr
description: Isr 拡張機能では、指定したアドレスに Itanium 中断状態の登録 (ISR) が表示されます。
ms.assetid: 35cf1749-2417-4fd9-9de2-0884ee795ab3
keywords:
- ISR (中断状態の登録)
- 中断状態のレジスタ (ISR)
- Windows デバッグ isr
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- isr
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bc29562a30e3b857ee4415a483c13d37a47d62f2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573268"
---
# <a name="isr"></a>!isr


! Isr 拡張機能では、指定したアドレスに Itanium 中断状態の登録 (ISR) が表示されます。

```dbgcmd
!isr Expression [DisplayLevel]
```

**重要な**  このコマンドが 10.0.14257 Windows デバッガーのバージョンでは非推奨以降されてし、は現在利用できません。

 

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Expression______"></span><span id="_______expression______"></span><span id="_______EXPRESSION______"></span> *式*   
表示する ISR レジスタの 16 進数のアドレスを指定します。 式<strong>@isr</strong>このパラメーターにも使用できます。 その場合は、ISR 登録、現在のプロセッサに関する情報が表示されます。

<span id="_______DisplayLevel______"></span><span id="_______displaylevel______"></span><span id="_______DISPLAYLEVEL______"></span> *DisplayLevel*   
次のオプションのいずれかを指定できます。

<span id="0"></span>**0**  
各 ISR フィールドの値のみが表示されます。 既定値です。

<span id="1"></span>**1**  
詳細については予約済みまたは無視されていない ISR フィールドを表示します。

<span id="2"></span>**2**  
無視するか予約されているものも含め、すべての ISR フィールドの詳細を表示します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>利用不可</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

この拡張機能のコマンドは、Itanium のターゲット コンピューターでのみ使用できます。

<a name="remarks"></a>コメント
-------

この拡張機能からの出力の例をいくつか次に示します。

```dbgcmd
kd> !isr @isr
isr:ed ei so ni ir rs sp na r w x vector code
  0  0  0  0  0  0  0  0 0 0 0      0   0

kd> !isr @isr 2

 cod : 0 : interruption Code
 vec : 0 : IA32 exception vector number
  rv : 0 : reserved0
   x : 0 : eXecute exception
   w : 0 : Write exception
   r : 0 : Read exception
  na : 0 : Non-Access exception
  sp : 0 : Speculative load exception
  rs : 0 : Register Stack
  ir : 0 : Invalid Register frame
  ni : 0 : Nested Interruption
  so : 0 : IA32 Supervisor Override
  ei : 0 : Exception IA64 Instruction
  ed : 0 : Exception Deferral
  rv : 0 : reserved1
```

 

 





