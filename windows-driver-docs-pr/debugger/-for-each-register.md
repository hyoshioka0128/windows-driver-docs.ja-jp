---
title: for_each_register
description: For_each_register 拡張機能は、各レジスタを指定したコマンドを実行します。
ms.assetid: 496DC161-D082-4C83-A6B6-6BBCE932BE76
keywords:
- Windows デバッグ for_each_register
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- for_each_register
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3e3d8e42aa26416006e772ae0e1e83486b306d56
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538655"
---
# <a name="foreachregister"></a>! の\_各\_登録


**! の\_各\_登録**拡張機能は、各レジスタを指定したコマンドを実行します。

```dbgcmd
!for_each_register -c:CommandString
!for_each_register -?
```

## <a name="span-idddkforeachmoduledbgspanspan-idddkforeachmoduledbgspanparameters"></a><span id="ddk__for_each_module_dbg"></span><span id="DDK__FOR_EACH_MODULE_DBG"></span>パラメーター


<span id="_______-c_CommandString______"></span><span id="_______-c_commandstring______"></span><span id="_______-C_COMMANDSTRING______"></span> **-c:**<em>クラスヒント</em>   
各レジスタに実行するコマンドを指定します。 @ エイリアス\#RegisterName および @\#コマンドの実行中に RegisterValue は無効です。

<span id="_______-_______"></span> **-?**   
ヘルプを表示、 **! の\_各\_登録**拡張機能。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Ext.dll

## <a name="span-idexamplesspanspan-idexamplesspanspan-idexamplesspanexamples"></a><span id="Examples"></span><span id="examples"></span><span id="EXAMPLES"></span>例


この例では、各登録の名前が一覧表示します。

```dbgcmd
0:000> !for_each_register -c:.echo @#RegisterName
rax
rcx
rdx
rbx
...
```

この例では実行[ **! アドレス**](-address.md)ごとに値を登録します。

```dbgcmd
0:000> !for_each_register -c:!address ${@#RegisterValue}
...
Usage:                  Stack
Base Address:           00000008`a568f000
End Address:            00000008`a56a0000
Region Size:            00000000`00011000
State:                  00001000    MEM_COMMIT
Protect:                00000004    PAGE_READWRITE
Type:                   00020000    MEM_PRIVATE
Allocation Base:        00000008`a5620000
Allocation Protect:     00000004    PAGE_READWRITE
More info:              ~0k
...
```

<a name="remarks"></a>注釈
-------

エイリアスがデバッガー拡張機能への引数の場合 (たとえば、 [ **! アドレス**](-address.md))、エイリアスのインタープリターを使用して、 [ **${} (別名インタープリター)**](-------alias-interpreter-.md)トークンのエイリアスが正しく解決できるようにします。

定義および文字の文字列を入力するためのショートカットとしてエイリアスを使用する方法の詳細 (の使用を含む、 [ **${}**  ](-------alias-interpreter-.md)トークン) を参照してください[Using エイリアス](using-aliases.md).

 

 





