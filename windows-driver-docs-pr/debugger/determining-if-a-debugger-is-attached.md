---
title: デバッガーがアタッチされているかどうかの判別
description: デバッガーがアタッチされているかどうかの判別
ms.assetid: 78f7d90a-459c-4967-a980-3f8d6339eb77
keywords:
- デバッガーがアタッチされているかどうかを決定します。
- KdRefreshDebuggerNotPresent function
- KD_DEBUGGER_ENABLED グローバル変数
- KD_DEBUGGER_NOT_PRESENT グローバル変数
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 90e6bddc42dc2ce5b0edb4eab70a6f6c4d0c507c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346305"
---
# <a name="determining-if-a-debugger-is-attached"></a>デバッガーがアタッチされているかどうかの判別


## <span id="ddk_determining_if_a_debugger_is_attached_dbg"></span><span id="DDK_DETERMINING_IF_A_DEBUGGER_IS_ATTACHED_DBG"></span>


カーネル モード コードには、次の変数とルーチンを使用してカーネル デバッグの状態を確認できます。

-   KD\_デバッガー\_有効カーネルのグローバル変数は、カーネルのデバッグが有効になっているかどうかを示します。

-   KD\_デバッガー\_いない\_存在のカーネルのグローバル変数は、カーネル デバッガーが現在接続されているかどうかを示します。

-   (Windows Server 2003 以降)**KdRefreshDebuggerNotPresent**ルーチン KD の値を更新する\_デバッガー\_いない\_存在します。

完全なドキュメントについては、Windows ドライバー キットを参照してください。

 

 





