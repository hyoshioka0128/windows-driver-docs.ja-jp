---
title: .dml_flow (Unasemmble リンクを含む)
description: .Dml_flow コマンドでは、逆アセンブルしたコード ブロックを表示し、コード フロー グラフを作成するために使用できるリンクを提供します。
ms.assetid: 32B50228-05A5-4BA7-88B1-54D4E502EB85
keywords:
- .dml_flow (Unasemmble リンクを含む) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .dml_flow (Unasemmble with Links)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 46dea3bdf71325eeb3a65621d66fa68aeb98abba
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580275"
---
# <a name="dmlflow-unasemmble-with-links"></a>.dml\_フロー (Unasemmble リンクを含む)


**.Dml\_フロー**コマンドは、逆アセンブルしたコード ブロックを表示し、コード フロー グラフを作成するために使用できるリンクを提供します。

```dbgcmd
.dml_flow Start Target
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="Start"></span><span id="start"></span><span id="START"></span>*開始*  
ターゲット アドレスが到達可能命令のアドレス。

<span id="Target"></span><span id="target"></span><span id="TARGET"></span>*ターゲット*  
逆アセンブルするコード ブロックのアドレス。

<a name="remarks"></a>コメント
-------

次の例に示すように、呼び出し履歴を検討してください。

```dbgcmd
0: kd> kL
Child-SP          RetAddr           Call Site
fffff880`0335c688 fffff800`01b41f1c nt!IofCallDriver
fffff880`0335c690 fffff800`01b3b6b4 nt!IoSynchronousPageWrite+0x1cc
fffff880`0335c700 fffff800`01b4195e nt!MiFlushSectionInternal+0x9b8
...
```

先頭からのすべてのコード パスを確認したいとします**nt!MiFlushSectionInternal**戻り値のアドレスを含むコード ブロックに`` fffff800`01b3b6b4 ``します。 次のコマンドは、開始します。

```dbgcmd
.browse .dml_flow nt!MiFlushSectionInternal fffff800`01b3b6b4
```

出力で、[コマンド ブラウザー ウィンドウ](command-browser-window.md)、次の図に示します。

![.dml のスクリーン ショット\-出力のフロー](images/dmlflow01.png)

上記の図は、ターゲット アドレスを含むコード ブロック`` fffff800`01b3b6b4 ``します。 1 つだけのリンクがある (`` fffff800`01b3b681 ``) イメージの上部にあります。 現在のコード ブロックをアクセスできる 1 つだけのコード ブロックがあることを示します。 リンクをクリックした場合、コード ブロックを逆アセンブル、およびさらに、コードのフロー グラフを表示するためのリンクが表示されますが表示されます。

上の図の下部にある 2 つのリンクは、現在のコード ブロックから到達可能な 2 つのコード ブロックがあることを示します。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[デバッガーのマークアップ言語コマンド](debugger-markup-language-commands.md)

[**uf (Unasemmble 関数)**](uf--unassemble-function-.md)

 

 






