---
title: KD のデバッグ セッションを終了します。
description: KD のデバッグ セッションを終了します。
ms.assetid: 6CD39971-424D-4F29-9A36-CCD14187DEB0
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d114286fd8ebfc1e2f2bfe8e8eeba0a255c7586
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552518"
---
# <a name="ending-a-debugging-session-in-kd"></a>KD のデバッグ セッションを終了します。


KD を終了する 2 つのさまざまな方法はあります。

-   問題を[ **q (終了)** ](q--qq--quit-.md) KD ログ ファイルを保存、デバッグ セッションを終了し、デバッガーを終了するコマンド。 ターゲット コンピューターがロックされたままにします。

-   キーを押して[ **CTRL + B** ](ctrl-b--quit-local-debugger-.md)し、enter キーを押してデバッガーを突然終了します。 対象のコンピュータ、デバッガーが終了した後に実行を継続する場合は、このメソッドを使用する必要があります。 CTRL + B は、ブレークポイントを削除しないことを最初に、次のコマンドを使用する必要があります。

    ```dbgcmd
    kd>  bc *
    kd>  g
    ```

CTRL キーを押しながら B キーを使用して、デバッガーを終了するカーネル モードのブレークポイントをクリアしませんが、新しいカーネル デバッガーをアタッチすると、これらのブレークポイントはクリアされます。

リモート デバッグ、実行している場合[ **q** ](q--qq--quit-.md)デバッグ セッションは終わります。 Ctrl キーを押しながら B は、デバッガーを終了が、セッションをアクティブなままです。 このような状況では、セッションに接続する別のデバッガーを使用できます。

場合、 [ **q (終了)** ](q--qq--quit-.md)コマンドは機能しません、キーを押して[ **CTRL + R** ](ctrl-r--re-synchronize-.md)とは、ホスト コンピューターのキーボードで ENTER キーを押しますを再試行して、**q**コマンド。 この手順が機能しない場合は、デバッガーを終了します CTRL キーを押しながら B キーを使用する必要があります。

 

 





