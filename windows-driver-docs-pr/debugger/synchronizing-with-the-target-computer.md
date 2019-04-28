---
title: ターゲット コンピューターとの同期
description: ターゲット コンピューターとの同期
ms.assetid: bc9bbe35-6665-49ee-ba95-16ff03e25e96
keywords:
- 対象のコンピュータとの同期
- 対象のコンピュータとの同期の概要
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: e739d249ee1356490e7166413055894b1e2427f9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368138"
---
# <a name="synchronizing-with-the-target-computer"></a>ターゲット コンピューターとの同期


## <span id="ddk_synchronizing_with_the_target_computer_dbg"></span><span id="DDK_SYNCHRONIZING_WITH_THE_TARGET_COMPUTER_DBG"></span>


カーネル モードのデバッグ、実行中には、ターゲット コンピューターは、デバッガーへの応答を停止します。

KD のキーを押して[ **(再同期) CTRL + R** ](ctrl-r--re-synchronize-.md)と対象のコンピューターに同期するには ENTER を押します。 WinDbg を使用して[CTRL + ALT + R](debug---kernel-connection---resynchronize.md)またはデバッグ |カーネルの接続 |再同期します。

これらのコマンドは、ホストとターゲット間の通信を頻繁に復元します。 ただし、再同期は常に失敗する、カーネルの 1394 接続を使用している場合に特に。

[ **.Restart (再起動カーネル接続)** ](-restart--restart-kernel-connection-.md)コマンドが再同期のより強力なメソッドを提供します。 このコマンドは、デバッガーを終了し、既存のセッションに新しいデバッガーをアタッチと同じです。 このコマンドは、WinDbg ではなく KD でのみ使用可能です。

**.Restart**コマンドは、実行している場合、最も役に立つ[remote.exe を通じてリモート デバッグ](remote-debugging-through-remote-exe.md)します。 (でこの種のデバッグには、そのにくい可能性を終了し、デバッガーを再起動します。)ただし、使用することはできません **.restart**デバッガーからのリモート デバッグを実行している場合、デバッグのクライアントから。

 

 





