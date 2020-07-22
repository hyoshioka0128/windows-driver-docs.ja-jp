---
title: デバッガーがアタッチされているかどうかの判別
description: デバッガーがアタッチされているかどうかの判別
ms.assetid: 78f7d90a-459c-4967-a980-3f8d6339eb77
keywords:
- デバッガーがアタッチされているかどうかを確認する
- KdRefreshDebuggerNotPresent 関数
- KD_DEBUGGER_ENABLED グローバル変数
- KD_DEBUGGER_NOT_PRESENT グローバル変数
ms.date: 07/20/2020
ms.localizationpriority: medium
ms.openlocfilehash: 7c863634de0c18803471035717b75c16a2516675
ms.sourcegitcommit: 3ec971f54122b77408433f7f1e59c467099fb4de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/21/2020
ms.locfileid: "86873857"
---
# <a name="determining-if-a-debugger-is-attached"></a>デバッガーがアタッチされているかどうかの判別

カーネルモードのコードでは、次の変数とルーチンを使用してカーネルデバッグの状態を確認できます。

- [**KD \_ デバッガーが \_ 有効になっ**](https://docs.microsoft.com/previous-versions/ff548118(v=vs.85))ているグローバルカーネル変数は、カーネルデバッグが有効になっているかどうかを示します。

- [**KD \_ デバッガー \_ \_ **](https://docs.microsoft.com/previous-versions/ff548125(v=vs.85))のグローバルカーネル変数は、カーネルデバッガーが現在アタッチされているかどうかを示します。

- [**KdRefreshDebuggerNotPresent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kdrefreshdebuggernotpresent)ルーチンは、KD \_ デバッガーが存在しない値を更新し \_ \_ ます。
