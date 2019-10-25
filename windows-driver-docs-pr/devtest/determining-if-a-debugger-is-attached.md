---
title: デバッガーがアタッチされているかどうかの判別
description: デバッガーがアタッチされているかどうかの判別
ms.assetid: b40482c4-7186-4632-b1d9-3c91a415b7c8
keywords:
- コードをデバッグする WDK、アタッチされたデバッガー
- アタッチされたデバッガー WDK
- 状態情報 WDK デバッグ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc3dc5c034c6e26646c9e929cadaa9d1f934186d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840282"
---
# <a name="determining-if-a-debugger-is-attached"></a>デバッガーがアタッチされているかどうかの判別


## <span id="ddk_determining_if_a_debugger_is_attached_tools"></span><span id="DDK_DETERMINING_IF_A_DEBUGGER_IS_ATTACHED_TOOLS"></span>


カーネルデバッガーが現在アタッチされている場合は、ドライバーに対して特定のアクションを実行することをお勧めします。

カーネルデバッグの状態を確認するには、次の変数とルーチンが役立ちます。

-   (Microsoft Windows XP 以降)[**KD\_DEBUGGER\_enabled**](https://docs.microsoft.com/previous-versions/ff548118(v=vs.85))グローバルカーネル変数は、カーネルデバッグが有効になっているかどうかを示します。

-   (Windows XP 以降)[**KD\_デバッガー\_\_存在しない**](https://docs.microsoft.com/previous-versions/ff548125(v=vs.85))グローバルカーネル変数は、カーネルデバッガーが現在アタッチされているかどうかを示します。

-   (Microsoft Windows Server 2003 以降)[**KdRefreshDebuggerNotPresent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kdrefreshdebuggernotpresent)ルーチンは、KD\_デバッガーの値を更新し\_\_存在しません。

 

 





