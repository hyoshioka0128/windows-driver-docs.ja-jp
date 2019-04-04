---
title: カーネル モードの Visual Studio でのデバッグ
description: Microsoft Visual Studio でのカーネル モード デバッグを実行するには
ms.assetid: 6E77843F-4907-4193-B987-92BD0719AE10
keywords:
- カーネル モードの visual studio のデバッグ
ms.date: 05/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5f77678509680cb79b1a780bef3580dc210133ef
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531838"
---
# <a name="span-iddebuggerperformingkernel-modedebuggingusingvisualstudiospankernel-mode-debugging-in-visual-studio"></a><span id="debugger.performing_kernel-mode_debugging_using_visual_studio"></span>カーネル モードの Visual Studio でのデバッグ

> [!IMPORTANT]
> この機能は、Windows 10 バージョン 1507、以降のバージョンの WDK でご利用いただけません。
>


Microsoft Visual Studio でのカーネル モード デバッグを実行するには。

1.  Visual Studio で、ホスト コンピューター上の**ツール**] メニューの [選択**プロセスにアタッチ**。
2.  **プロセスにアタッチ**ダイアログ ボックスで、セット**トランスポート**に**Windows カーネル モードのデバッガー**、設定と**修飾子**の名前に、以前の構成済みの対象のコンピュータ。 ターゲット コンピューターの構成方法の詳細については、[カーネル モード デバッグのセットアップでは、Visual Studio](setting-up-kernel-mode-debugging-in-visual-studio.md)または[カーネル モード デバッグ手作業でセットアップ](setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md)を参照してください。
3.  クリックして**アタッチします。**

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Visual Studio を使用したデバッグ](debugging-using-visual-studio.md)

 

 






