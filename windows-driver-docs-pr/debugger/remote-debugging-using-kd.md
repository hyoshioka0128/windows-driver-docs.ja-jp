---
title: リモートのデバッグを使用して KD
description: リモート デバッグには、2 つの異なる場所で実行されている 2 つのデバッガーが含まれます。
ms.assetid: 274CAB1D-DD3B-4ACD-919C-8B8C253BCE50
ms.date: 05/03/2018
ms.localizationpriority: medium
ms.openlocfilehash: cb9663cd1b172140bb461d55cc2e1748645facb4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535787"
---
# <a name="remote-debugging-using-kd"></a>リモートのデバッグを使用して KD


リモート デバッグには、2 つの異なる場所で実行されている 2 つのデバッガーが含まれます。 デバッグを実行する、デバッガーが呼び出され、*サーバー デバッグ*します。 呼ばれる、2 つ目のデバッガー、*デバッグ クライアント*、リモートの場所から、デバッグ セッションを制御します。 リモート セッションを確立するには、まずデバッグ サーバーを設定し、デバッグのクライアントを有効にする必要があります。

リモート デバッグは、PC でデバッグしている問題を調べて、他のユーザーが関係したい場合に役立ちます。

デバッグのサーバーを実行している同じコンピューターには、デバッグ中のコードが実行される可能性がまたは別のコンピューターで実行されている可能性があります。 デバッグ サーバーが実行する場合、ユーザー モードのデバッグは、デバッグ中のプロセスがデバッグ サーバーと同じコンピューターで実行できます。 デバッグ サーバーには、カーネル モードのデバッグが実行して、別のターゲット コンピューターでデバッグ中のコードは実行通常します。

次の図は、ホスト コンピューター上で実行、デバッグ サーバーが別のターゲット コンピューターで実行されているコードのカーネル モードのデバッグを実行は、リモート セッションを示しています。

![リモートを示す図、ホスト、および対象のコンピューター](images/clientservertarget.png)

いくつかのトランスポート プロトコルをリモート デバッグ接続を使用することがあります。TCP、NPIPE、SPIPE、SSL、および COM ポート。 プロトコルとして TCP を使用しているし、デバッグのクライアントとデバッグ サーバーの両方として KD を使用するいるとします。 カーネル モードのリモート デバッグ セッションを確立するために、次の手順を使用できます。

1. ホスト コンピューターでは、KD を開き、対象のコンピュータとカーネル モードのデバッグ セッションを確立します。 (を参照してください[KD を使用してカーネル モードのデバッグを実行する](performing-kernel-mode-debugging-using-kd.md))。
2. CRTL Break キーを押して中断します。
3. 次のコマンドを入力します。

   **.server tcp:port=5005**

   **注**5005 ポート番号は任意です。 ポート番号は、あなた次第です。

     

4. KD は、次のような出力で応答します。

   ```dbgcmd
   Server started.  Client can connect with any of these command lines
   0: <debugger> -remote tcp:Port=5005,Server=YourHostComputer
   ```

5. リモート コンピューターでは、コマンド プロンプト ウィンドウを開き、次のコマンドを入力します。

   **kd-リモート tcp:Port 5005、サーバーの = =**<em>YourHostComputer</em>

   場所*YourHostComputer*デバッグ サーバーを実行しているホスト コンピューターの名前を指定します。

## <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報


起動 KD (および確立するリモート デバッグ)、コマンドラインでの詳細については、次を参照してください。 [ **KD コマンド ライン オプション**](kd-command-line-options.md)します。

 

 





