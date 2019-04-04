---
title: teb
description: Teb 拡張機能では、スレッド環境ブロックの終了の情報の書式設定されたビューが表示されます。
ms.assetid: 4137b54b-f784-412d-bffd-e8a71a54155e
keywords:
- Windows デバッグ teb
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- teb
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1bbfca1dfe2d16695faa052a590706864d8d03ee
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529550"
---
# <a name="teb"></a>! teb


**! Teb**拡張機能では、スレッド環境ブロックの終了の情報の書式設定されたビューが表示されます。

```dbgcmd
!teb [TEB-Address] 
```

## <a name="span-idddktebdbgspanspan-idddktebdbgspanparameters"></a><span id="ddk__teb_dbg"></span><span id="DDK__TEB_DBG"></span>パラメーター


<span id="_______TEB-Address______"></span><span id="_______teb-address______"></span><span id="_______TEB-ADDRESS______"></span> *TEB アドレス*   
スレッドを調べるの TEB の 16 進数のアドレス。 (これはないスレッドのカーネルのスレッドのブロックから派生したとして TEB のアドレス。)場合*TEB アドレス*がユーザー モードで、TEB 省略すると、現在のスレッドが使用されます。 かどうかは、カーネル モードでは、現在に対応する TEB で省略[コンテキストを登録](changing-contexts.md#register-context)が表示されます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Exts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

スレッド環境ブロックについては、*Microsoft Windows internals 』* Mark Russinovich と David Solomon を参照してください。

<a name="remarks"></a>注釈
-------

TEB は、Microsoft Windows のスレッドの制御構造のユーザー モードの部分です。

場合、 **! teb**引数なしで拡張機能、エラーを表示カーネル モードでは、使用する必要があります、 [ **! プロセス**](-process.md)拡張機能を目的のスレッドの TEB アドレスを決定します。 確認、[コンテキストを登録](changing-contexts.md#register-context)が目的のスレッドに設定し、引数として TEB アドレスを使用 **! teb**します。

ユーザー モードでこのコマンドの出力の例を次に示します。

```dbgcmd
0:001> ~
   0  id: 324.458   Suspend: 1 Teb 7ffde000 Unfrozen
.  1  id: 324.48c   Suspend: 1 Teb 7ffdd000 Unfrozen

0:001> !teb 
TEB at 7FFDD000
    ExceptionList:    76ffdc
    Stack Base:       770000
    Stack Limit:      76f000
    SubSystemTib:     0
 FiberData:        1e00
    ArbitraryUser:    0
    Self:             7ffdd000
    EnvironmentPtr:   0
 ClientId:         324.48c
    Real ClientId:    324.48c
    RpcHandle:        0
    Tls Storage:      0
    PEB Address:      7ffdf000
    LastErrorValue:   0
    LastStatusValue:  0
    Count Owned Locks:0
    HardErrorsMode:   0
```

同様、 [ **! peb** ](-peb.md)拡張機能は、プロセスの環境ブロックを表示します。

 

 





