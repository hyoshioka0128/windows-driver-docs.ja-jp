---
title: グローバル変数へのアクセス
description: グローバル変数へのアクセス
ms.assetid: 81daf418-d3cf-413a-8ee0-790b0c0f86c0
keywords:
- グローバル変数
- グローバル変数へのアクセス
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7e736328bc8e355ea75b6da5a87985fa3a48606
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572411"
---
# <a name="accessing-global-variables"></a>グローバル変数へのアクセス


## <span id="ddk_debugging_bios_code_dbg"></span><span id="DDK_DEBUGGING_BIOS_CODE_DBG"></span>


グローバル変数の名前は、アプリケーションをコンパイルするときに作成されるシンボル ファイルに格納されます。 デバッガーは、仮想アドレスとして、グローバル変数の名前を解釈します。 また、アドレスをパラメーターとして受け入れる任意のコマンドは、変数の名前を受け入れます。 すべての記載されているコマンドを使用するため、[仮想アドレスにアクセスするメモリ](accessing-memory-by-virtual-address.md)グローバル変数を読み書きします。

さらに、使用、 [**でしょうか。(式の評価)** ](---evaluate-expression-.md)任意のシンボルに関連付けられているアドレスを表示するコマンド。

Visual Studio と WinDbg の表示し、グローバル変数を編集する (コマンド) だけでなく使用できるユーザー インターフェイス要素を提供します。 参照してください[メモリとレジスタ Visual Studio で表示および編集](viewing-memory--variables--and-registers-in-visual-studio.md)と[の表示と編集 WinDbg でグローバル変数](viewing-and-editing-global-variables-in-windbg.md)します。

次の例を検討してください。 確認すると、`MyCounter`グローバル変数は、32 ビット整数します。 また、既定の基数は 10 であるとします。

この変数のアドレスを取得し、次のように表示できます。

```dbgcmd
0:000> ? MyCounter 
Evaluate expression: 1244892 = 0012fedc
0:000> dd 0x0012fedc L1 
0012fedc  00000052
```

最初のコマンド出力動いているのアドレス`MyCounter`0x0012FEDC です。 使用することができますし、 [ **d\* (メモリの表示)** ](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)このアドレスに 1 つのダブル ワードを表示するコマンド。 (使用することも 1244892、このアドレスの 10 進数バージョンであります。 ただし、ほとんどの C プログラマ使用したい 0x0012FEDC。)2 番目のコマンドは、MyCounter の値が 0x52 (10 進 82) を指示します。

次のコマンドで次の手順を実行することもできます。

```dbgcmd
0:000> dd MyCounter L1 
0012fedc  00000052
```

値を変更する`MyCounter`10 進数の 83 に次のコマンドを使用します。

```dbgcmd
0:000> ed MyCounter 83 
```

この例は、その形式が、整数のより自然なので、10 進数の入力を使用します。 ただしの出力、 [ **d\\**  * ](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)コマンドは、16 進数形式のままにします。

```dbgcmd
0:000> dd MyCounter L1 0012fedc  00000053
```

 

 





