---
title: デバッガーがアタッチされているかどうかの判別
description: デバッガーがアタッチされているかどうかの判別
ms.assetid: b40482c4-7186-4632-b1d9-3c91a415b7c8
keywords:
- デバッガーがアタッチされている WDK コードのデバッグ
- WDK のアタッチされたデバッガー
- 状態情報の WDK のデバッグ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5bb9b33f6ee3ce0571adba5e75ec593e37b3624
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371410"
---
# <a name="determining-if-a-debugger-is-attached"></a>デバッガーがアタッチされているかどうかの判別


## <span id="ddk_determining_if_a_debugger_is_attached_tools"></span><span id="DDK_DETERMINING_IF_A_DEBUGGER_IS_ATTACHED_TOOLS"></span>


カーネル デバッガーが現在アタッチされている場合に、ドライバーの特定のアクションを実行したい場合があります。

カーネル デバッグの状態を確認するには、次の変数とルーチンは役立ちます。

-   (Microsoft Windows XP 以降)[ **KD\_デバッガー\_有効**](https://docs.microsoft.com/previous-versions/ff548118(v=vs.85))カーネルのグローバル変数は、カーネルのデバッグが有効になっているかどうかを示します。

-   (Windows XP 以降)[ **KD\_デバッガー\_いない\_存在**](https://docs.microsoft.com/previous-versions/ff548125(v=vs.85))カーネルのグローバル変数は、カーネル デバッガーが現在接続されているかどうかを示します。

-   (Microsoft Windows Server 2003 以降)[ **KdRefreshDebuggerNotPresent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kdrefreshdebuggernotpresent)ルーチン KD の値を更新する\_デバッガー\_いない\_存在します。

 

 





