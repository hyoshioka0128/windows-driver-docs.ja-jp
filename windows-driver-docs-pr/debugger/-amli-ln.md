---
title: amli ln
description: Amli ln 拡張機能には、指定したメソッドまたは特定のアドレスを格納しているメソッドが表示されます。
ms.assetid: f763f185-cce2-4bfb-948d-243acfb53aaa
keywords:
- Windows デバッグ amli ln
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- amli ln
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 34a302d69631437aa883d8c077aab7b516ce41ab
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334757"
---
# <a name="amli-ln"></a>!amli ln


**! Amli ln**拡張機能は、指定したメソッドまたは特定のアドレスを格納しているメソッドが表示されます。

構文

```dbgcmd
    !amli ln [ MethodName | CodeAddress ]
```

## <a name="span-idddkamlilndbgspanspan-idddkamlilndbgspanparameters"></a><span id="ddk__amli_ln_dbg"></span><span id="DDK__AMLI_LN_DBG"></span>パラメーター


<span id="_______MethodName______"></span><span id="_______methodname______"></span><span id="_______METHODNAME______"></span> *methodName*   
メソッド名の完全なパスを指定します。 場合*MethodName*実際には、メソッド、エラーの結果ではないオブジェクトを指定します。

<span id="_______CodeAddress______"></span><span id="_______codeaddress______"></span><span id="_______CODEADDRESS______"></span> *CodeAddress*   
希望の方法に含まれている AML コードのアドレスを指定します。 場合*CodeAddress*に 2 つのパーセント記号が付いています (**%%**)、物理アドレスとして解釈されます。 それ以外の場合、その仮想アドレスとして解釈されます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

関連するコマンドとその用途については、次を参照してください。 [AMLI デバッガー](the-amli-debugger.md)します。

<a name="remarks"></a>注釈
-------

どちらの場合*MethodName*も*CodeAddress*を指定すると、現在のコンテキストに関連付けられたメソッドが表示されます。

次のコマンドは、現在実行されているメソッドを示します。

```console
kd> !amli ln
c29accf5: \_WAK
```

メソッド\_アドレス 0xC29ACCF5 WAK を表示します。

 

 





