---
title: u、ub、uu (Unassemble)
description: U * コマンドは、指定されたプログラムコードのアセンブリ変換をメモリ内に表示します。 このコマンドは、~ u (スレッドの凍結解除) コマンドと混同しないようにしてください。
ms.assetid: 933a308c-61d1-4ca4-89c1-5749ba1b41c1
keywords:
- u、ub、uu (Unassemble) Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- u, ub, uu (Unassemble)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6b0931b1ff3ef4b7a3be6f97b948edf44d2808a0
ms.sourcegitcommit: d5f54510b9500413dd3084b59cb8869f2f6b13cf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68866762"
---
# <a name="u-ub-uu-unassemble"></a>u、ub、uu (Unassemble)


**U\\** * コマンドは、指定されたプログラムコードのアセンブリ変換をメモリ内に表示します。

このコマンドは、 [ **~ u (スレッドの凍結解除)** ](-u--unfreeze-thread-.md)コマンドと混同しないようにしてください。

```dbgcmd
u[u|b] Range 
u[u|b] Address
u[u|b] 
```

## <a name="span-idddk_cmd_unassemble_dbgspanspan-idddk_cmd_unassemble_dbgspanparameters"></a><span id="ddk_cmd_unassemble_dbg"></span><span id="DDK_CMD_UNASSEMBLE_DBG"></span>パラメータ


<span id="_______Range______"></span><span id="_______range______"></span><span id="_______RANGE______"></span>*範囲*   
逆アセンブルする命令を含むメモリ範囲を指定します。 構文の詳細については、「[アドレスとアドレス範囲の構文](address-and-address-range-syntax.md)」を参照してください。 **B**フラグを使用する場合は、"*Address1 Address2*" 構文ではなく "*Address* **L**_Length_" 構文を使用して*範囲*を指定する必要があります。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*アドレス*   
逆アセンブルするメモリ範囲の先頭を指定します。 8つの命令 (x86 ベースのプロセッサの場合) または9つの命令 (Itanium ベースのプロセッサの場合) は、アセンブルされません。 構文の詳細については、「[アドレスとアドレス範囲の構文](address-and-address-range-syntax.md)」を参照してください。

<span id="_______b______"></span><span id="_______B______"></span>**b**   
逆方向にカウントすることによって逆アセンブルするメモリ範囲を決定します。 **Ub** *address*が使用されている場合、逆アセンブルされた範囲は、*アドレス*で終わる8または9バイト範囲になります。 範囲が指定されている場合は、 **ub** *アドレス* **L**の_長さ_は、指定された長さの範囲の終了*アドレス*。

<span id="_______u______"></span><span id="_______U______"></span>**u**   
メモリ読み取りエラーが発生した場合でも逆アセンブルを続行することを指定します。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>Environment

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>ユーザーモード、カーネルモード</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ、クラッシュダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>・</strong></p></td>
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

アセンブリデバッグと関連コマンドの詳細については、「[アセンブリモードでのデバッグ](debugging-in-assembly-mode.md)」を参照してください。

<a name="remarks"></a>コメント
-------

**U**コマンドのパラメーターを指定しない場合、逆アセンブリは現在のアドレスから開始し、8命令 (x86 ベースまたは x64 ベースのプロセッサの場合) または9命令 (Itanium ベースのプロセッサの場合) を拡張します。 パラメーターを指定せずに**ub**を使用すると、逆アセンブリには、現在のアドレスの前に8または9の命令が含まれます。

このコマンドを[**up (物理メモリからアセンブル解除)** ](up--unassemble-from-physical-memory-.md)と混同しないでください。 **U**コマンドを実行すると、仮想メモリのみが逆アセンブルされますが、 **up**コマンドでは物理メモリのみが逆アセンブルされます。

 

 





