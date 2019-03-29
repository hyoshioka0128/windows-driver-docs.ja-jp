---
title: 中間のシンボル
description: 中間のシンボル
ms.assetid: 0fbf47fc-1216-4eaa-b4b9-96e206194b54
keywords:
- 3 番目のコンピューターでリモート デバッグ、シンボル
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7fe0bc98fe140a1b68a1defb57b61c2c976928e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574261"
---
# <a name="symbols-in-the-middle"></a>中間のシンボル


## <span id="ddk_symbols_in_the_middle_dbg"></span><span id="DDK_SYMBOLS_IN_THE_MIDDLE_DBG"></span>


このシナリオでは、3 台のコンピューターがあります。 最初のターゲット アプリケーション、2 番目は、シンボルがあり、3 番目の技術者です。

スマート クライアントは、すべての方法で通常のデバッガーのように動作であるため、できますデバッグ サーバーとして同時に。 これにより、中央のスマート クライアントと共に、3 つのマシンをリンクすることができます。

最初に、コンピューターでプロセス サーバーを起動\\\\ボックス。

```console
dbgsrv -t npipe:pipe=FarPipe 
```

という名前の中間のマシン\\ \\BOXB が両方と、デバッガーを起動、 **-premote**と **-サーバー**パラメーター。 対象アプリケーションの PID が 400 とシンボル パスが g:\\MySymbols:

```console
cdb -server npipe:pipe=NearPipe -premote npipe:server=BOXA,pipe=FarPipe -v -y g:\mysymbols -p 400 
```

次のように 3 つ目のコンピューターでのデバッグのクライアントを開始することができます。

```console
windbg -remote npipe:server=BOXB,pipe=NearPipe 
```

3 番目のマシンは、デバッグ、2 つ目のマシンは、実際の処理は行われ、シンボルにアクセスを制御し、使用されます。

 

 





