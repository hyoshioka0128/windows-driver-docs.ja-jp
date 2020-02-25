---
title: グローバル変数へのアクセス
description: グローバル変数へのアクセス
ms.assetid: 81daf418-d3cf-413a-8ee0-790b0c0f86c0
keywords:
- グローバル変数
- グローバル変数、アクセス
ms.date: 02/20/2020
ms.localizationpriority: medium
ms.openlocfilehash: 2ce50b8367571ea03e4ee718c64b79a112ed71d9
ms.sourcegitcommit: d03c24342b9852013301a37e2ec95592804204f1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2020
ms.locfileid: "77528930"
---
# <a name="accessing-global-variables"></a>グローバル変数へのアクセス


## <span id="ddk_debugging_bios_code_dbg"></span><span id="DDK_DEBUGGING_BIOS_CODE_DBG"></span>


グローバル変数の名前は、アプリケーションのコンパイル時に作成されるシンボルファイルに格納されます。 デバッガーは、グローバル変数の名前を仮想アドレスとして解釈します。 パラメーターとしてアドレスを受け取るすべてのコマンドは、変数の名前も受け入れます。 したがって、「[仮想アドレスによるメモリ](accessing-memory-by-virtual-address.md)へのアクセス」で説明されているすべてのコマンドを使用して、グローバル変数の読み取りまたは書き込みを行うことができます。

また、を使用することもでき[**ます。(式の評価)** ](---evaluate-expression-.md)コマンドを使用して、任意のシンボルに関連付けられているアドレスを表示します。

WinDbg には、グローバル変数を表示および編集するために (コマンドに加えて) 使用できるユーザーインターフェイス要素が用意されています。 「 [WinDbg でのグローバル変数の表示と編集」を](viewing-and-editing-global-variables-in-windbg.md)参照してください。

次の例について考えてみましょう。 32ビット整数である `MyCounter` グローバル変数を調べるとします。 また、既定の基数が10であるとします。

この変数のアドレスを取得して、次のように表示できます。

```dbgcmd
0:000> ? MyCounter 
Evaluate expression: 1244892 = 0012fedc
0:000> dd 0x0012fedc L1 
0012fedc  00000052
```

最初のコマンドの出力は、`MyCounter` のアドレスが0x0012FEDC であることを示しています。 その後、 [**d\* (Display Memory)** ](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)コマンドを使用して、このアドレスに1つのダブルワードを表示できます。 (このアドレスの10進数バージョンである1244892を使用することもできます。 ただし、ほとんどの C プログラマは、0x0012FEDC を使用します)。2番目のコマンドは、MyCounter の値が 0x52 (10 進 82) であることを示します。

これらの手順は、次のコマンドでも実行できます。

```dbgcmd
0:000> dd MyCounter L1 
0012fedc  00000052
```

`MyCounter` の値を10進数83に変更するには、次のコマンドを使用します。

```dbgcmd
0:000> ed MyCounter 83 
```

この例では、整数に対してより自然な形式であるため、10進入力を使用しています。 ただし、 [ **d\\** *](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)コマンドの出力は、16進形式のままです。

```dbgcmd
0:000> dd MyCounter L1 0012fedc  00000053
```

 

 





