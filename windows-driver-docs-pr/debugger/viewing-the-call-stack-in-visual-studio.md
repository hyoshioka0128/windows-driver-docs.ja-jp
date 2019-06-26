---
title: Visual Studio でのコール スタックの表示
description: プロシージャは、Visual Studio で呼び出し履歴を表示する方法を説明します。
ms.assetid: 060A2441-C1A7-4485-82E5-2C024E6A3FBE
ms.date: 05/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: a094c36fca13ac50a6f251713af3e4150758d4ba
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369465"
---
# <a name="viewing-the-call-stack-in-visual-studio"></a>Visual Studio でのコール スタックの表示

> [!IMPORTANT]
> この機能は、Windows 10 バージョン 1507、以降のバージョンの WDK でご利用いただけません。
>

このトピックで示す手順では、Visual Studio に統合された Windows Driver Kit が必要です。 統合環境を取得するには、最初に、Microsoft Visual Studio をインストールし、Windows Driver Kit (WDK) をインストールします。 詳細については、次を参照してください。 [Windows ドライバー開発](https://docs.microsoft.com/windows-hardware/drivers/)します。

## <a name="span-idusingthecallstackwindowspanspan-idusingthecallstackwindowspanspan-idusingthecallstackwindowspanusing-the-call-stack-window"></a><span id="Using_the_Call_Stack_Window"></span><span id="using_the_call_stack_window"></span><span id="USING_THE_CALL_STACK_WINDOW"></span>呼び出し履歴 ウィンドウを使用します。


開くには、**呼び出し履歴**Visual Studio で、ウィンドウから、**デバッグ**] メニューの [選択**Windows&gt;呼び出し履歴**します。 スタック トレースの表示で特定の行に、ローカル コンテキストを設定するには、行の最初の列をダブルクリックします。

## <a name="span-idviewingthecallstackbyenteringcommandsspanspan-idviewingthecallstackbyenteringcommandsspanspan-idviewingthecallstackbyenteringcommandsspanviewing-the-call-stack-by-entering-commands"></a><span id="Viewing_the_Call_Stack_by_Entering_Commands"></span><span id="viewing_the_call_stack_by_entering_commands"></span><span id="VIEWING_THE_CALL_STACK_BY_ENTERING_COMMANDS"></span>コマンドを入力して、呼び出し履歴を表示します。


いずれかを入力して、呼び出し履歴を表示する、デバッガーのイミディ エイト ウィンドウで、 [ **k (Display Stack Backtrace)** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)コマンド。 デバッガーのイミディ エイト ウィンドウが開いてからない場合、**デバッグ**] メニューの [選択**Windows&gt;イミディ エイト**します。

 

 





