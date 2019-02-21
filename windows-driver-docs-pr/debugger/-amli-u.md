---
title: amli u
description: Amli u 拡張機能は unassembles AML コードです。
ms.assetid: 0a8b160f-9aae-4ef0-a569-8e701de9679c
keywords:
- Windows デバッグ amli u
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- amli u
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5881f44ea1d07c28f0597561a5586402a49df28d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529747"
---
# <a name="amli-u"></a>! amli u


**! Amli u**拡張子 unassembles AML コード。

構文

```dbgcmd
    !amli u [ MethodName | CodeAddress ]
```

## <a name="span-idddkamliudbgspanspan-idddkamliudbgspanparameters"></a><span id="ddk__amli_u_dbg"></span><span id="DDK__AMLI_U_DBG"></span>パラメーター


<span id="_______MethodName______"></span><span id="_______methodname______"></span><span id="_______METHODNAME______"></span> *methodName*   
逆アセンブルする対象のメソッド名の完全なパスを指定します。

<span id="_______CodeAddress______"></span><span id="_______codeaddress______"></span><span id="_______CODEADDRESS______"></span> *CodeAddress*   
逆アセンブリの開始位置、AML コードのアドレスを指定します。 場合*CodeAddress*に 2 つのパーセント記号が付いています (**%%**)、物理アドレスとして解釈されます。 それ以外の場合、その仮想アドレスとして解釈されます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

関連するコマンドとその用途については、次を参照してください。 [AMLI デバッガー](the-amli-debugger.md)します。

<a name="remarks"></a>注釈
-------

どちらの場合*MethodName*も*CodeAddress*が指定されて、AMLI からこのコマンドを発行していると

逆アセンブリの表示は、メソッドの末尾に達するまでに続行されます。

**注**  標準[ **u (Unassemble)** ](u--unassemble-.md)コマンド AML コードで適切な結果に表示されなくなります。

 

例をいくつか紹介します。 アドレス 0x80E5D701 にあるオブジェクトを逆アセンブルするには、次のコマンドを使用します。

```console
kd> !amli u 80e5d701

ffffffff80e5d701 : CreateWordField(CRES, 0x1, IRQW)
ffffffff80e5d70c : And(\_SB_.PCI0.LPC_.PIRA, 0xf, Local0)
ffffffff80e5d723 : Store(One, Local1)
ffffffff80e5d726 : ShiftLeft(Local1, Local0, IRQW)
ffffffff80e5d72d : Return(CRES)
```

次のコマンドは逆アセンブル、 \_DCK メソッド。

```console
kd> u \_sb.pci0.dock._dck
```

 

 





