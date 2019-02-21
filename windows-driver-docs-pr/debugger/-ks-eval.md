---
title: ks.eval
description: Ks.eval 拡張機能は、拡張機能に固有の式エバリュエーターを使用して、式を評価します。
ms.assetid: 68c9cfb0-ff87-47ea-bd0d-5f45c1de0639
keywords:
- デバッグ ks.eval Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.eval
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8e5c02094509d424108666be077921e1daebc424
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528045"
---
# <a name="kseval"></a>!ks.eval


**! Ks.eval**拡張機能が拡張機能に固有の式エバリュエーターを使用して、式を評価します。

```dbgcmd
!ks.eval Expression 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Expression______"></span><span id="_______expression______"></span><span id="_______EXPRESSION______"></span> *式*   
評価する式を指定します。 *式*MASM 演算子、シンボル、または数値の構文を以下に示す拡張機能に固有の演算子を含めることができます。 MASM の式の詳細については、次を参照してください。 [MASM 数字と演算子](masm-numbers-and-operators.md)します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>winxp\Ks.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Ks.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、次を参照してください。[ストリーミングのカーネル デバッグ](kernel-streaming-debugging.md)します。

<a name="remarks"></a>注釈
-------

拡張機能モジュールには、拡張機能のコマンドにパラメーターをアドレスに使用できる 2 つの拡張機能に固有の演算子が含まれます。

<span id="________fdo_________x_________"></span><span id="________FDO_________X_________"></span> **fdo(** *x* **)**  
アドレスにあるオブジェクトに関連付けられている機能のデバイス オブジェクトを返します**x**します。

<span id="________driver_________x_________"></span><span id="________DRIVER_________X_________"></span> **driver(** *x* **)**  
関連付けられているドライバー オブジェクトを返します**fdo (**<em>x</em>**)** します。

使用することができます、 **! ks.eval**これらの拡張機能に固有の演算子を含む式を解析するコマンドだけでなく[MASM 数字と演算子](masm-numbers-and-operators.md)します。

サポートされるすべての演算子に注意してください **! ks.eval** Ks.dll 拡張モジュールで他のすべての拡張機能コマンドでもサポートされます。

次の例に示します、 **! ks.eval**フィルターのアドレスで使用されている拡張機能。 0x8241C020 アドレスの存在に注意してください、 [ **! ks.allstreams** ](-ks-allstreams.md)出力。

```dbgcmd
kd> !eval fdo(829493c4)
Resulting Evaluation: 8241c020

kd> !allstreams
6 Kernel Streaming FDOs found:
    Functional Device 82a17690 [\Driver\smwdm]
    Functional Device 8296eb08 [\Driver\wdmaud]
    Functional Device 82490388 [\Driver\sysaudio]
    Functional Device 82970cb8 [\Driver\MSPQM]
    Functional Device 824661b8 [\Driver\MSPCLOCK]
    Functional Device 8241c020 [\Driver\avssamp]
```

 

 





