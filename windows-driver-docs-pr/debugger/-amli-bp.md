---
title: amli bp
description: Amli bp 拡張機能は、AML コードにブレークポイントを配置します。
ms.assetid: 830df6b8-835c-4485-a28a-e9a028f166f5
keywords:
- Windows デバッグ amli bp
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- amli bp
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0b84fd4c9df4347cc9cf9915eb695fb20110c160
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581209"
---
# <a name="amli-bp"></a>!amli bp


**! Amli bp**拡張機能は、AML コードでブレークポイントを設定します。

構文

```dbgcmd
    !amli bp { MethodName | CodeAddress }
```

## <a name="span-idddkamlibpdbgspanspan-idddkamlibpdbgspanparameters"></a><span id="ddk__amli_bp_dbg"></span><span id="DDK__AMLI_BP_DBG"></span>パラメーター


<span id="_______MethodName______"></span><span id="_______methodname______"></span><span id="_______METHODNAME______"></span> *methodName*   
ブレークポイントを設定するメソッド名の完全なパスを指定します。

<span id="_______CodeAddress______"></span><span id="_______codeaddress______"></span><span id="_______CODEADDRESS______"></span> *CodeAddress*   
ブレークポイントを設定する AML コードのアドレスを指定します。 場合*CodeAddress*に 2 つのパーセント記号が付いています (**%%**)、物理アドレスとして解釈されます。 それ以外の場合、その仮想アドレスとして解釈されます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

関連するコマンドとその用途については、[AMLI デバッガー](the-amli-debugger.md)を参照してください。

<a name="remarks"></a>コメント
-------

AMLI デバッガーには、最大 10 個のブレークポイントがサポートしています。

次に例を示します。 次のコマンドにブレークポイントを設定、 \_DCK メソッド。

```console
kd> !amli bp \_sb.pci0.dock._dck
```

 

 





