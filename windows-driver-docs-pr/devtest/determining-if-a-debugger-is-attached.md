---
title: デバッガーがアタッチされているかどうかを決定します。
description: デバッガーがアタッチされているかどうかを決定します。
ms.assetid: b40482c4-7186-4632-b1d9-3c91a415b7c8
keywords:
- デバッガーがアタッチされている WDK コードのデバッグ
- WDK のアタッチされたデバッガー
- 状態情報の WDK のデバッグ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 953678bebd10bba2bec6dfbe31f3a5f8e960abf3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548580"
---
# <a name="determining-if-a-debugger-is-attached"></a>デバッガーがアタッチされているかどうかを決定します。


## <span id="ddk_determining_if_a_debugger_is_attached_tools"></span><span id="DDK_DETERMINING_IF_A_DEBUGGER_IS_ATTACHED_TOOLS"></span>


カーネル デバッガーが現在アタッチされている場合に、ドライバーの特定のアクションを実行したい場合があります。

カーネル デバッグの状態を確認するには、次の変数とルーチンは役立ちます。

-   (Microsoft Windows XP 以降)[ **KD\_デバッガー\_有効**](https://msdn.microsoft.com/library/windows/hardware/ff548118)カーネルのグローバル変数は、カーネルのデバッグが有効になっているかどうかを示します。

-   (Windows XP 以降)[ **KD\_デバッガー\_いない\_存在**](https://msdn.microsoft.com/library/windows/hardware/ff548125)カーネルのグローバル変数は、カーネル デバッガーが現在接続されているかどうかを示します。

-   (Microsoft Windows Server 2003 以降)[ **KdRefreshDebuggerNotPresent** ](https://msdn.microsoft.com/library/windows/hardware/ff548109)ルーチン KD の値を更新する\_デバッガー\_いない\_存在します。

 

 





