---
title: Repeater の例
description: Repeater の例
ms.assetid: 83aff647-65a7-409f-adce-254305395775
keywords:
- repeater、例
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a6dc91c7ba60ab880546da6fd293e7846c1d1ec
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550435"
---
# <a name="repeater-examples"></a>Repeater の例


## <span id="ddk_repeater_examples_dbg"></span><span id="DDK_REPEATER_EXAMPLES_DBG"></span>


3 台のコンピューターがあるとします知らせ\\\\ボックス、 \\ \\BOXB、および\\ \\BOXC、およびするが、それぞれ、サーバー、repeater、および、クライアントとして使用します。

デバッグ サーバーを開始する\\\\次のように、ターゲットとして 122 のプロセスを使用して、ボックス。

```console
E:\Debugging Tools for Windows> cdb -server tcp:port=1025,password=wrought -p 122 
```

Repeater を開始することができますし、 \\ \\BOXB として次のとおりです。

```console
C:\Misc> dbengprx -c tcp:server=BOXA,port=1025 -s npipe:pipe=MyPipe 
```

最後に、デバッグのクライアントを開始\\ \\BOXC 次のようにします。

```console
G:\Debugging Tools> windbg -remote npipe:server=BOXB,pipe=MyPipe,password=wrought 
```

別の例を次に示します。 127.0.0.30、リモートの場所で、シンボルとは。 したがって、ターゲットが、127.0.0.10 コンピューターでプロセス サーバーを使用すること。 127.0.0.20 には、repeater を配置します。

逆方向の接続を使用することもできます。 したがって 127.0.0.30 でクライアントを起動して開始します。

```console
G:\Debugging Tools> windbg -premote tcp:clicon=127.0.0.20,port=1033 notepad.exe 
```

127.0.0.20 で repeater を開始します。

```console
C:\Misc> dbengprx -c tcp:clicon=127.0.0.10,port=1025 -s tcp:port=1033,clicon=127.0.0.10 
```

127.0.0.10 で最後に、プロセス サーバーを起動します。

```console
E:\Debugging Tools for Windows> dbgsrv -t tcp:port=1025,clicon=127.0.0.20 
```

リピータを使用してより複雑な例は、次を参照してください。 [2 つのファイアウォール](two-firewalls.md)します。

 

 





