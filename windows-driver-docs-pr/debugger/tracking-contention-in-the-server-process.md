---
title: サーバー プロセス内の競合の追跡
description: サーバー プロセス内の競合の追跡
ms.assetid: ef0c0294-a010-439b-82dd-25148e05a7f1
keywords:
- RPC デバッグ、競合の追跡
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 041d8a089755a25fafb2586295b787fa2776081c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380792"
---
# <a name="tracking-contention-in-the-server-process"></a>サーバー プロセス内の競合の追跡


## <span id="ddk_tracking_contention_in_the_server_process_dbg"></span><span id="DDK_TRACKING_CONTENTION_IN_THE_SERVER_PROCESS_DBG"></span>


サービスの受信要求に順番は、RPC はワーカー スレッドのセットを維持します。 理想的には、スレッドの数のサイズは小さくなります。 ただし、この理想的な状況は、サーバー マネージャーのルーチンが慎重に調整されて、ラボ環境でのみ確認されています。 実際の状況では、スレッドの数はサーバーのワークロードによって異なりますが、50 に 1 から任意の場所にすることができます。

ワーカー スレッドの数が 50 を超える場合は、サーバー プロセスで過剰な競合があります。 この一般的な原因は、ヒープを区別しないで使用メモリの不足、または 1 つの重要なセクションを経由してサーバー内のアクティビティをシリアル化します。

特定のサーバー プロセスのスレッドの数を表示する、 [ **! rpcexts.getthreadinfo** ](-rpcexts-getthreadinfo.md)拡張機能、または使用させるために、 **-t**スイッチします。 (次の例では、0xC4) でプロセス ID を指定します。

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

この場合が 7 のワーカー スレッドは妥当です。

100 を超えるスレッドがある場合は、このプロセスと原因の調査に、デバッガーをアタッチする必要があります。

**注**  などのクエリを実行している**させるためには、-t**リモートでは、サーバーとネットワークのコスト。 スクリプトでこのクエリを使用する場合はこのコマンドは、多くの場合に実行されないことを確認する必要があります。

 

 

 





