---
title: RPC セル情報の取得
description: RPC セル情報の取得
ms.assetid: 7dd5e77e-914d-4b00-90c5-92705eebf436
keywords:
- RPC のセルの情報
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3fb6b3e72b260371fc342fa6e6738b3b2d8301f2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380234"
---
# <a name="get-rpc-cell-information"></a>RPC セル情報の取得


## <span id="ddk_get_rpc_cell_information_dbg"></span><span id="DDK_GET_RPC_CELL_INFORMATION_DBG"></span>


セルの詳細な情報を表示、 **! rpcexts.getdbgcell**拡張機能、またはさせるためときに、 **-l**スイッチを使用します。

セルの数、および、推奨されるセルを含むプロセスのプロセス ID を指定する必要があります。

次の例では、プロセス ID は 0x278、セルの数は 0000.0002 です。

```console
D:\wmsg>dbgrpc -l -P 278 -L 0.2
Getting cell info ...
Thread
Status: Dispatched
Thread ID: 0x1A4 (420)
Last update time (in seconds since boot):470.25 (0x1D6.19)
```

省略可能なパラメーターの詳細については、「 [**させるためのコマンド ライン オプション**](dbgrpc-command-line-options.md)します。

デバッガーの拡張機能の RPC を使用して類似の例については、「 [ **! rpcexts.getdbgcell**](-rpcexts-getdbgcell.md)します。

 

 





