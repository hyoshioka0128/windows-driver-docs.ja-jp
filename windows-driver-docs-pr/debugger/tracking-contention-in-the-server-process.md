---
title: サーバー プロセス内の競合の追跡
description: サーバー プロセス内の競合の追跡
ms.assetid: ef0c0294-a010-439b-82dd-25148e05a7f1
keywords:
- RPC デバッグ, 競合の追跡
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 935cad63601665b2f24e98809497c48514600e61
ms.sourcegitcommit: 958a5ced83856df22627c06eb42c9524dd547906
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83235421"
---
# <a name="tracking-contention-in-the-server-process"></a>サーバー プロセス内の競合の追跡


## <span id="ddk_tracking_contention_in_the_server_process_dbg"></span><span id="DDK_TRACKING_CONTENTION_IN_THE_SERVER_PROCESS_DBG"></span>


受信要求を処理するために、RPC は一連のワーカースレッドを保持します。 理想的には、スレッドの数は小さくなります。 ただし、この理想的な状況はラボ環境でのみ見られ、サーバーマネージャールーチンは慎重にチューニングされています。 実際の状況では、スレッドの数はサーバーのワークロードによって異なりますが、1 ~ 50 の任意の場所に配置できます。

ワーカースレッドの数が50を超えると、サーバープロセスで過剰な競合が発生する可能性があります。 一般的な原因は、ヒープの使用、メモリの負荷、または1つの重要なセクションを通じてサーバー内のほとんどのアクティビティをシリアル化することです。

特定のサーバープロセスのスレッド数を確認するには、 [**! rpcexts**](-rpcexts-getthreadinfo.md)拡張機能を使用するか、 **-t**スイッチで dbgrpc を使用します。 プロセス ID を指定します (次の例では、0xC4)。

```console
D:\wmsg>dbgrpc -t -P c4
Searching for thread info ...
## PID  CELL ID   ST TID      LASTTIME
-----------------------------------
00c4 0000.0004 03 0000011c 000f164f
00c4 0000.0007 03 00000120 008a6290
00c4 0000.0015 03 0000018c 008a6236
00c4 0000.0026 03 00000264 0005c443
00c4 0000.002d 03 00000268 000265bb
00c4 0000.0030 03 0000026c 000f1d32
00c4 0000.0034 03 00000388 007251e9
```

この場合、ワーカースレッドは7つしかありません。

100を超えるスレッドがある場合は、このプロセスにデバッガーをアタッチし、原因を調査する必要があります。

**メモ**   **Dbgrpc-t**などのクエリをリモートで実行すると、サーバーとネットワークに負荷がかかります。 このクエリをスクリプトで使用する場合は、このコマンドが頻繁に実行されないようにする必要があります。

 

 

 





