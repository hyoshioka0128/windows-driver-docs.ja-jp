---
title: 2 つのファイアウォール
description: 2 つのファイアウォール
ms.assetid: e6192cf8-02a4-4dbe-8ed7-a64f8efc24f6
keywords:
- リモート デバッグ、2 つのファイアウォール
- ファイアウォールとリモート デバッグ
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c79f520a6a6d767a660fd20c2d4b382eb7b9b9a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380780"
---
# <a name="two-firewalls"></a>2 つのファイアウォール


## <span id="ddk_two_firewalls_dbg"></span><span id="DDK_TWO_FIREWALLS_DBG"></span>


このシナリオでは、カーネル A. の建物内のコンピューターでのデバッグを実行する必要があります。技術者は、建物の C にあるし、ユーザーがシンボルへのアクセスがあります。 ただし、両方のビルは、着信接続を許可しないファイアウォールがあります。

ニュートラル サイト--ビルド B.、repeater を設定する必要があります。外向きを B に接続して B に C 外側への接続

4 台のコンピューターをこのシナリオに関連できるようになります。

-   A. の建物内にある、対象のコンピューター

-   A. の建物内にある、ローカル ホスト コンピューターこのコンピューターは KD 接続のサーバーで実行されます。 デバッグ ケーブルまたは 1394 ケーブルの場合は、ターゲット コンピューターに接続し、repeater に外側へ接続します。 このコンピューターの IP アドレスが 127.0.10.10 をすることができます。

-   B. の建物内のコンピューターこれにより、リピータが実行されます。 127.0.20.20 する IP アドレスを使用できます。

-   技術者のあるビルド C でのコンピューター。 このコンピューターは、WinDbg をスマート クライアントとして実行されます。 127.0.30.30 する IP アドレスを使用できます。

まず、対象のコンピューターがデバッグ用に構成され、ローカル ホスト コンピューターに接続されたことを確認してください。 この例では、1394 ケーブルを使用します。

次に、127.0.20.20 で repeater を起動します。

```console
dbengprx -p -s tcp:port=9001 -c tcp:port=9000,clicon=127.0.10.10 
```

第 3 に、サーバーを起動 KD 接続 127.0.10.10 A の建物内で、次のように。

```console
kdsrv -t tcp:port=9000,clicon=127.0.20.20,password=longjump 
```

最後に、ビルドの c 言語で 127.0.30.30 でスマート クライアントを開始します。(これは実際に行えます前に、またはビルド A. でサーバーを起動した後)

```console
windbg -k kdsrv:server=@{tcp:server=127.0.20.20,port=9001,password=longjump},trans=@{1394:channel=9} -y SymbolPath
```

### <a name="span-idfivecomputerscenariospanspan-idfivecomputerscenariospanfive-computer-scenario"></a><span id="five_computer_scenario"></span><span id="FIVE_COMPUTER_SCENARIO"></span>5 台のコンピューターのシナリオ

このシナリオにできるさらに複雑な場合は、シンボルは、建物の c 言語で 1 台のコンピューターが、技術者が別のコンピューターにだと思います。

127.0.30.30 が以前のように、シンボルとそのローカル名がある\\ \\BOXC します。 上記と同じコマンドではなく、追加、スマート クライアントを開始できる **-サーバー**パラメーター。 このマシンを使用できないために WinDbg ではなく KD を使用する場合は、処理時間がかかるは。

```console
kd -server npipe:pipe=randomname -k kdsrv:server=@{tcp:server=127.0.20.20,port=9001,password=longjump},trans=@{1394:channel=9} -y SymbolPath
```

技術者は、構築、他の場所でできますデバッグ クライアントよう開始。

```console
windbg -remote npipe:server=\\BOXC,pipe=randomname 
```

最初以外、repeater、チェーン内でパスワードを渡す必要があることに注意してください (上のスマート クライアント\\ \\BOXC) チェーン内の最終的なデバッガーではなく、します。

 

 





