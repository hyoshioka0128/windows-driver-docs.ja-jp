---
title: RPC スレッド情報を取得します。
description: RPC スレッド情報を取得します。
ms.assetid: 4cb8d11f-5b0a-4526-9f64-ee69fd15d1ba
keywords:
- RPC スレッド情報
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: cbee1913f1dd40f0d4a27809e611f781a2d1bde7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527996"
---
# <a name="get-rpc-thread-information"></a>RPC スレッド情報を取得します。


## <span id="ddk_get_rpc_thread_information_dbg"></span><span id="DDK_GET_RPC_THREAD_INFORMATION_DBG"></span>


によってスレッドの情報が表示されます、 **! rpcexts.getthreadinfo**拡張機能、またはさせるため、ときに、 **-t**スイッチを使用します。

プロセスの PID を指定する必要があります。 そのプロセス内のスレッドを指定することがあります。 スレッドを省略すると、そのプロセス内のすべてのスレッドが表示されます。

次の例では、スレッド ID を省略してプロセス ID が 0x278:

```console
D:\wmsg>dbgrpc -t -P 278
Searching for thread info ...
## PID  CELL ID   ST TID      LASTTIME
-----------------------------------
0278 0000.0002 01 000001a4 00072c09
0278 0000.0005 03 0000031c 00072bf5
```

省略可能なパラメーターの詳細については、「 [**させるためのコマンド ライン オプション**](dbgrpc-command-line-options.md)します。

デバッガーの拡張機能の RPC を使用して類似の例については、「 [ **! rpcexts.getthreadinfo**](-rpcexts-getthreadinfo.md)します。

 

 





