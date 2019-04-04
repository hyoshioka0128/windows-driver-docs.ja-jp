---
title: リモートのデバッグを使用して WinDbg
description: リモート デバッグには、2 つの異なる場所で実行されている 2 つのデバッガーが含まれます。
ms.assetid: 3030CEE4-DF10-4F84-A32D-38613D7EE072
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c4ec56f7332a46adc31879859fcf0e0d1703438
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557210"
---
# <a name="remote-debugging-using-windbg"></a>リモートのデバッグを使用して WinDbg


リモート デバッグには、2 つの異なる場所で実行されている 2 つのデバッガーが含まれます。 デバッグを実行する、デバッガーが呼び出され、*サーバー デバッグ*します。 呼ばれる、2 つ目のデバッガー、*デバッグ クライアント*、リモートの場所から、デバッグ セッションを制御します。 リモート セッションを確立するには、まずデバッグ サーバーを設定し、デバッグのクライアントを有効にする必要があります。

デバッグのサーバーを実行している同じコンピューターには、デバッグ中のコードが実行される可能性がまたは別のコンピューターで実行されている可能性があります。 デバッグ サーバーが実行する場合、ユーザー モードのデバッグは、デバッグ中のプロセスがデバッグ サーバーと同じコンピューターで実行できます。 デバッグ サーバーには、カーネル モードのデバッグが実行して、別のターゲット コンピューターでデバッグ中のコードは実行通常します。

次の図は、ホスト コンピューター上で実行、デバッグ サーバーが別のターゲット コンピューターで実行されているコードのカーネル モードのデバッグを実行は、リモート セッションを示しています。

![リモートを示す図、ホスト、および対象のコンピューター](images/clientservertarget.png)

いくつかのトランスポート プロトコルをリモート デバッグ接続を使用することがあります。TCP、NPIPE、SPIPE、SSL、および COM ポート。 プロトコルとして TCP を使用しているし、デバッグのクライアントとデバッグ サーバーの両方として WinDbg を使用するいるとします。 カーネル モードのリモート デバッグ セッションを確立するために、次の手順を使用できます。

1. ホスト コンピューターでは、WinDbg を開き、対象のコンピュータとカーネル モードのデバッグ セッションを確立します。 (を参照してください[WinDbg を使用してカーネル モードのデバッグを Live](performing-kernel-mode-debugging-using-windbg.md))。
2. 選択して中断**中断**から、**デバッグ**メニューまたは Ctrl + break キーを押します。
3. [デバッガー コマンド ウィンドウ](debugger-command-window.md)、次のコマンドを入力します。

   **.server tcp:port=5005**

   **注**5005 ポート番号は任意です。 ポート番号は、あなた次第です。

     

4. WinDbg は、次のような出力で応答します。

   ```dbgcmd
   Server started.  Client can connect with any of these command lines
   0: <debugger> -remote tcp:Port=5005,Server=YourHostComputer
   ```

5. リモート コンピューターでは、WinDbg を開き**リモート セッションに接続する**から、**ファイル**メニュー。
6. **接続文字列**、次の文字列を入力します。

   **tcp:Port 5005、サーバーの = =**<em>YourHostComputer</em>

   場所*YourHostComputer*デバッグ サーバーを実行しているホスト コンピューターの名前を指定します。

   **[OK]** をクリックします。

## <a name="span-idusingthecommandlinespanspan-idusingthecommandlinespanspan-idusingthecommandlinespanusing-the-command-line"></a><span id="Using_the_Command_Line"></span><span id="using_the_command_line"></span><span id="USING_THE_COMMAND_LINE"></span>コマンドラインを使用


前のセクションの手順を代わりには、コマンドラインでのリモート デバッグ セッションを設定することができます。 チャネル 32 で 1394 ケーブルを介してホスト コンピューターと対象のコンピューター間でカーネル モードのデバッグ セッションを確立するために設定するとします。 リモート デバッグ セッションを確立するために、次の手順を使用できます。

1. ホスト コンピューターには、コマンド プロンプト ウィンドウで、次のコマンドを入力します。

   **windbg -server tcp:port=5005 -k 1394:channel=32**

2. リモート コンピューターでは、コマンド プロンプト ウィンドウで、次のコマンドを入力します。

   **windbg-リモート tcp:Port 5005、サーバーの = =**<em>YourHostComputer</em>

   場所*YourHostComputer*デバッグ サーバーを実行しているホスト コンピューターの名前を指定します。

## <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報


リモート デバッグのこのトピックに示すもの以外の場合を確立するために多くの方法はあります。 デバッグ、WinDbg でサーバーをセットアップする詳細については[デバッガー コマンド ウィンドウ](debugger-command-window.md)を参照してください[ **.server (デバッグ サーバーの作成)**](-server--create-debugging-server-.md)します。 起動 WinDbg (および確立するリモート デバッグ)、コマンドラインでの詳細については、[ **WinDbg コマンド ライン オプション**](windbg-command-line-options.md)を参照してください。

 

 





