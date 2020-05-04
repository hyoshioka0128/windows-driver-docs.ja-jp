---
title: WinDbg を使用したリモート デバッグ
description: リモートデバッグには、2つの異なる場所で実行される2つのデバッガーが含まれます。
ms.assetid: 3030CEE4-DF10-4F84-A32D-38613D7EE072
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c4ec56f7332a46adc31879859fcf0e0d1703438
ms.sourcegitcommit: 44bccc9788690ae636b17d7d1cc576b8a17c9916
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81727440"
---
# <a name="remote-debugging-using-windbg"></a>WinDbg を使用したリモート デバッグ


リモートデバッグには、2つの異なる場所で実行される2つのデバッガーが含まれます。 デバッグを実行するデバッガーは、*デバッグサーバー*と呼ばれます。 *デバッグクライアント*と呼ばれる2番目のデバッガーは、リモートの場所からデバッグセッションを制御します。 リモートセッションを確立するには、まずデバッグサーバーをセットアップしてから、デバッグクライアントをアクティブにする必要があります。

デバッグ対象のコードは、デバッグサーバーを実行しているのと同じコンピューター上で実行されている場合もあれば、別のコンピューターで実行されている場合もあります。 デバッグサーバーでユーザーモードのデバッグを実行している場合は、デバッグ中のプロセスをデバッグサーバーと同じコンピューターで実行できます。 デバッグサーバーでカーネルモードのデバッグを実行している場合は、通常、デバッグ対象のコードが別のターゲットコンピューターで実行されます。

次の図は、ホストコンピューター上で実行されているデバッグサーバーが、別のターゲットコンピューターで実行されているコードのカーネルモードデバッグを実行しているリモートセッションを示しています。

![リモートコンピューター、ホストコンピューター、および対象コンピューターを示す図](images/clientservertarget.png)

リモートデバッグ接続に使用できるトランスポートプロトコルには、TCP、NPIPE、SPIPE、SSL、COM ポートのいくつかがあります。 プロトコルとして TCP を使用することを選択し、デバッグクライアントとデバッグサーバーの両方として WinDbg を使用することを選択したとします。 リモートカーネルモードのデバッグセッションを確立するには、次の手順に従います。

1. ホストコンピューターで、WinDbg を開き、対象のコンピューターでカーネルモードのデバッグセッションを確立します。 (「 [WinDbg を使用したカーネルモードのライブデバッグ」を](performing-kernel-mode-debugging-using-windbg.md)参照してください)。
2. [**デバッグ**] メニューの [**中断**] をクリックするか、CTRL + Break キーを押して中断します。
3. デバッガーの[コマンドウィンドウ](debugger-command-window.md)で、次のコマンドを入力します。

   **。サーバー tcp: ポート = 5005**

   **メモ** ポート番号5005は任意です。 ポート番号は任意です。

     

4. WinDbg は、次のような出力で応答します。

   ```dbgcmd
   Server started.  Client can connect with any of these command lines
   0: <debugger> -remote tcp:Port=5005,Server=YourHostComputer
   ```

5. リモートコンピューターで、[WinDbg] を開き、[**ファイル**] メニューの [**リモートセッションに接続**] を選択します。
6. [**接続文字列**] に、次の文字列を入力します。

   **tcp: Port = 5005、Server = 自分の**<em>hostcomputer</em>

   ここで、 *Hostcomputer*は、デバッグサーバーを実行しているホストコンピューターの名前です。

   **[OK]** をクリックします。

## <a name="span-idusing_the_command_linespanspan-idusing_the_command_linespanspan-idusing_the_command_linespanusing-the-command-line"></a><span id="Using_the_Command_Line"></span><span id="using_the_command_line"></span><span id="USING_THE_COMMAND_LINE"></span>コマンドラインの使用


前のセクションで説明した手順の代わりに、コマンドラインでリモートデバッグセッションを設定することもできます。 たとえば、1394ケーブルを使用し32て、ホストコンピューターとターゲットコンピューターの間で、カーネルモードのデバッグセッションを確立するように設定しているとします。 リモートデバッグセッションを確立するには、次の手順に従います。

1. ホストコンピューターで、コマンドプロンプトウィンドウに次のコマンドを入力します。

   **windbg-サーバー tcp: ポート = 5005 1394: channel = 32**

2. リモートコンピューターで、コマンドプロンプトウィンドウに次のコマンドを入力します。

   **windbg-リモート tcp: ポート = 5005、Server = 自分の**<em>hostcomputer</em>

   ここで、 *Hostcomputer*は、デバッグサーバーを実行しているホストコンピューターの名前です。

## <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報


このトピックに記載されている以外に、リモートデバッグを確立するにはさまざまな方法があります。 WinDbg[デバッガーコマンドウィンドウ](debugger-command-window.md)でのデバッグサーバーの設定の詳細については、「 [**. サーバー (デバッグサーバーの作成)**](-server--create-debugging-server-.md)」を参照してください。 コマンドラインで WinDbg を起動する (およびリモートデバッグを確立する) 方法の詳細については、「 [**windbg のコマンドラインオプション**](windbg-command-line-options.md)」を参照してください。

 

 





