---
title: RPC デバッガー拡張機能の使用
description: RPC デバッガー拡張機能の使用
ms.assetid: 55303052-c5b3-4fe7-96ce-6f41a45a2358
keywords:
- RPC 拡張機能 (rpcexts.dll)
- RPC 拡張機能 (rpcexts.dll) をデバッグします。
- rpcexts.dll (RPC 拡張)
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: a84f5da0e299935045e4b029f3441e743763dc71
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340484"
---
# <a name="using-the-rpc-debugger-extensions"></a>RPC デバッガー拡張機能の使用


## <span id="ddk_using_the_rpc_debugger_extensions_dbg"></span><span id="DDK_USING_THE_RPC_DEBUGGER_EXTENSIONS_DBG"></span>


さまざまな RPC デバッガー拡張機能は、Rpcexts.dll からエクスポートされます。

RPC 状態情報を表示するために使用する RPC 拡張機能は、ユーザー モードでのみ実行されます。 これらは、CDB (、NTSD) またはユーザー モード WinDbg から使用できます。

ユーザー モード デバッガーは、ターゲット アプリケーションをいる必要がありますが、ターゲットが RPC 拡張機能に関連するではありません。 デバッガーが実行されていない場合は、始めることができますだけですが、不要なターゲット (たとえば、 **windbg メモ帳**または**cdb winmine**)。 使用して、 [ **CTRL + C** ](ctrl-c--break-.md) CDB でまたは[デバッグ |中断](debug---break.md)に WinDbg デバッガー コマンド] ウィンドウにアクセスをターゲットを停止します。

リモート コンピューターからの RPC 状態情報を分析する必要がある場合を分析し、使用する必要があるコンピューターのユーザー モード デバッガーを起動する必要があります[リモート デバッグ](remote-debugging.md)します。

デバッガーから RPC 状態情報へのアクセスは、ストレスの環境で、またはデバッガーが既に実行されているような場合に特に便利です。

 

 





