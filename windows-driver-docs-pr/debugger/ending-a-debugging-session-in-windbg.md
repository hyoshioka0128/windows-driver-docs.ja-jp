---
title: WinDbg のデバッグ セッションの終了
description: WinDbg のデバッグ セッションの終了
ms.assetid: 9C19211B-38CC-482B-B69F-B83B29963B3F
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3406b5ecef7d23eb740093b99942bfdf382dd182
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340597"
---
# <a name="ending-a-debugging-session-in-windbg"></a>WinDbg のデバッグ セッションの終了


## <a name="span-idexitingwindbgspanspan-idexitingwindbgspanspan-idexitingwindbgspanexiting-windbg"></a><span id="Exiting_WinDbg"></span><span id="exiting_windbg"></span><span id="EXITING_WINDBG"></span>WinDbg を終了します。


WinDbg を終了するを選択して**終了**から、**ファイル**メニューまたは alt キーを押しながら F4 キーを押します。

使用しない限り、これらのコマンドでをデバッグしているアプリケーションを閉じますユーザー モードのデバッグを実行する場合、 **-pd**デバッガーを起動したときに、コマンド ライン オプション。

カーネル モードのデバッグを実行する場合、対象のコンピュータは、現在の状態に残ります。 このような状況では、ターゲットのままにできます。 または固定されたを実行します。 (固定されているターゲットにした場合、カーネル デバッガーからの今後の接続を再開できます中断したところをデバッグします。)

## <a name="span-idendingausermodesessionwithoutexitingspanspan-idendingausermodesessionwithoutexitingspanending-a-user-mode-session-without-exiting"></a><span id="ending_a_user_mode_session_without_exiting"></span><span id="ENDING_A_USER_MODE_SESSION_WITHOUT_EXITING"></span>ユーザー モードのセッションを終了する前に終了


ユーザー モードのデバッグ セッションを終了するには、デバッガーを休止モードに戻る、およびターゲット アプリケーションを閉じるには、次のメソッドを使用することができますを。

-   入力、 [ **.kill (プロセスの強制終了)** ](-kill--kill-process-.md)コマンド。

-   入力、 [ **q (終了)** ](q--qq--quit-.md)コマンド (を使用してデバッガーを開始していない限り、 **-pd**オプション)。

-   選択**デバッグの停止**から、**デバッグ**メニュー。
-   SHIFT + F5 キーを押します。

-   をクリックして、**デバッグの停止**ボタン (![ボタンのデバッグの停止のスクリーン ショット](images/tbstop.png)) ツールバー

ユーザー モードのデバッグ セッションを終了するには、休止モードでは、もう一度実行している対象アプリケーションを次のメソッドを使用するにデバッガーを返します。

-   入力、 [ **.detach (プロセスからデタッチ)** ](-detach--detach-from-process-.md)コマンド。 複数のターゲットをデバッグする場合、このコマンドは、現在のターゲットからデタッチされ、残りのターゲットを使用してデバッグ セッションが続行されます。

-   選択**デバッグ対象のデタッチ**から、**デバッグ**メニュー。 複数のターゲットをデバッグする場合、このコマンドは、現在のすべてのターゲットからデタッチします。

-   入力、 [ **qd (Quit およびデタッチ)** ](qd--quit-and-detach-.md)コマンド。

-   入力、 [ **q (終了)** ](q--qq--quit-.md)コマンドを使用してデバッガーを開始した場合、 **-pd**オプション。

ユーザー モードのデバッグ セッションを終了、デバッガーを休止モードに戻るには、対象のアプリケーション デバッグ状態のままに、次のメソッドを使用することができます。

-   入力、 [ **.abandon (破棄プロセス)** ](-abandon--abandon-process-.md)コマンド。

ターゲットに再アタッチ方法の詳細については、次を参照してください。[対象アプリケーションを再アタッチ](reattaching-to-the-target-application.md)します。

## <a name="span-idendingakernel-modesessionwithoutexitingspanspan-idendingakernel-modesessionwithoutexitingspanspan-idendingakernel-modesessionwithoutexitingspanending-a-kernel-mode-session-without-exiting"></a><span id="Ending_a_Kernel-Mode_Session_Without_Exiting"></span><span id="ending_a_kernel-mode_session_without_exiting"></span><span id="ENDING_A_KERNEL-MODE_SESSION_WITHOUT_EXITING"></span>カーネル モードのセッションを終了する前に終了


カーネル モードのデバッグ セッションを終了して、デバッガーを休止モードに戻る固定されているターゲット コンピューターのままにするには、次のメソッドを使用できます。

-   入力、 [ **q (終了)** ](q--qq--quit-.md)コマンド (を使用してデバッガーを開始していない限り、 **-pd**オプション)

-   選択**デバッグの停止**から、**デバッグ**メニュー。
-   SHIFT + F5 キーを押します。

-   をクリックして、 **(Shift + F5) のデバッグを停止**ボタン (![ボタンのデバッグの停止のスクリーン ショット](images/tbstop.png)) ツールバー。

WinDbg のセッションの終了時に、現在のセッションのワークスペースを保存するように求められます、休止モードに WinDbg を返します。 この時点では、開始のすべてのオプションを使用することができます。 つまり、実行中のプロセスをデバッグ、新しいプロセスの生成、ターゲット コンピューターに接続、クラッシュ ダンプを開くかリモート デバッグ セッションに接続を開始することができます。

 

 





