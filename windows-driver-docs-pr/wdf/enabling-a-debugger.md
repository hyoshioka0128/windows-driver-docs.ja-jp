---
title: UMDF ドライバーのデバッグを有効にする方法
description: UMDF ドライバーのデバッグを有効にする方法
ms.assetid: ea37eb7b-09fa-4c8d-aff7-273b07bc0007
keywords:
- WDK UMDF をデバッガーします。
- デバッガーを有効にする、WDK UMDF
- ユーザー モード ドライバー フレームワーク WDK は、デバッガーを有効にします。
- UMDF WDK、デバッガーを有効にします。
- ユーザー モード ドライバー WDK UMDF、デバッガーを有効にします。
- デバッガーを有効にすると、WDK UMDF ドライバーのデバッグ
- デバッグ、デバッガーを有効にすると、WDK UMDF ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c692d332d7b19367b62fc27e289f77bfff28e69
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536621"
---
# <a name="how-to-enable-debugging-of-a-umdf-driver"></a>UMDF ドライバーのデバッグを有効にする方法


次の構成を使用して、ユーザー モード ドライバー フレームワーク (UMDF) ドライバーをデバッグすることができます。 すべての構成には、2 つのマシン、ホストとターゲットが含まれます。 ホスト コンピューターでは、ドライバーのビルドをインストールして、ターゲット コンピューターでドライバーをテストするには、Microsoft Visual Studio と Windows Driver Kit (WDK) を実行するとします。

-   (「展開」) をコピーする Visual Studio を使用してターゲットを開始するには、ホストで Visual Studio 内でのデバッグ セッションをユーザー モード ドライバー。
-   手動でドライバーをターゲットにコピーします。 ターゲットでユーザー モードのデバッグを実行します。 このシナリオでは、適用する手動でターゲットで実行されているドライバーのホスト プロセスのインスタンスにします。
-   ターゲットにドライバーを手動でコピーし、ホストからカーネル モードのデバッグを実行します。

一緒に使用する後者の 2 つの構成、ターゲット上のユーザー モード デバッガーとカーネル モード デバッガーの両方をホストで実行されています。

## <a href="" id="bp"></a>ベスト プラクティス


すべての UMDF ドライバーのカーネル デバッガーをアタッチでのテストを実行することをお勧めします。

推奨の設定を以下にします。 これらを手動で設定したり、使用して、 [WDF Verifier コントロール アプリケーション](https://msdn.microsoft.com/library/windows/hardware/ff556129)(WDFVerifier.exe) ツールで、WDK を表示またはこれらの設定を変更します。

-   WUDFHost.exe で Application Verifier を有効にします。

    ```cpp
    AppVerif –enable Heaps Exceptions Handles Locks Memory TLS Leak –for WudfHost.exe
    ```

    例外が発生した場合 Application Verifier はデバッガーに診断メッセージを送信しで中断されます。

-   有効にする[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)します。 開く、**コマンド プロンプト**ウィンドウ (**管理者として実行**)。 ドライバー検証ツール マネージャーを開くことの検証方法を入力します。
-   カーネル モードのデバッグ セッションを使用している場合は、設定**HostFailKdDebugBreak**リフレクターが、ドライバーのホスト プロセスを終了する前にカーネル モード デバッガーを中断できるようにします。 この設定は、UMDF バージョン 1.11 以降を既定で有効です。

-   設定してプールを無効に**UmdfHostProcessSharing**に**ProcessSharingDisabled**します。 については、[INF ファイルで WDF ディレクティブを指定する](specifying-wdf-directives-in-inf-files.md)を参照してください。
-   既定では、UMDF デバイスが失敗したときに、フレームワークの設定は最大 5 回再起動を試行します。 自動再起動をオフに設定して**DebugModeFlags** 0x01 にします。 詳細については、[デバッグ WDF のドライバーのレジストリ値](registry-values-for-debugging-kmdf-drivers.md)を参照してください。
-   お使いのコンピューターを再起動します。

## <a name="using-visual-studio-with-f5-to-attach-automatically-user-mode-debugging"></a>F5 キーを押して Visual Studio を使用して自動的にアタッチする (ユーザー モードのデバッグ)


WDK で Visual Studio を使用して、テスト コンピューター上のドライバーをデバッグすることができます、最初を設定してテスト マシンを構成します。 これを行う方法については、[テスト コンピューターにドライバーを展開する](https://msdn.microsoft.com/windows-drivers/develop/deploying_a_driver_to_a_test_computer)を参照してください。

テスト用コンピューターを構成した後、ホスト コンピューターで Visual Studio を使用して、ドライバーにブレークポイントを設定します。 F5 キーを押すと、Visual Studio は、ドライバーをビルド、対象のコンピューターに展開しますされ、ユーザー モードのデバッグ セッションを開始します。

この手法を使用して、UMDF ドライバーを展開するときに、Visual Studio がオン*UMDF デバッグ モード*ドライバー。 既定では、デバッグ モードはことを意味します。

-   ドライバーは、独自の専用のホスト プロセスで起動します。 [デバイスのプール](using-device-pooling-in-umdf-drivers.md)は無効になります。
-   ドライバー クラッシュ後にデバイスが自動的に再起動しないと、エラー報告を無効にします。
-   フレームワークで説明されているタイムアウトは強制されません[UMDF でホスト プロセスのタイムアウト](how-umdf-enforces-time-outs.md)します。
-   UMDF ホスト プロセスまたはフレームワーク verifier は、無効な操作を検出する場合、UMDF はユーザー モード デバッガーを中断します。

デバッグ モードを使用して、ドライバーのインストールには、再起動が必要です。 場合でも、UMDF ドライバーをデバッグすることができます。 生体認証、スマート カード、または入力例で、ユーザーがログオンする前に開始するユーザー モード ドライバーをデバッグすることもできます。

## <a name="using-windbg-to-attach-manually-user-mode-debugging"></a>WinDbg を使用して手動でアタッチする (ユーザー モードのデバッグ)


ターゲット コンピューターでは、ドライバーをホストする WUDFHost のインスタンスに WinDbg を手動でアタッチできます。 アタッチすると、デバッガーを中断して、ドライバーでブレークポイントを設定することができます。

ドライバーの初期化の直後に発生するため WUDFHost を読み込む、初期化コードをデバッグする時間を手動でアタッチすることはできません。 代わりに、ホスト プロセスがいくつかのホストの初期化またはドライバーの読み込み時に秒の待機にレジストリ値を設定することができます。 この遅延は、WinDbg を WUDFHost プロセスの適切なインスタンスにアタッチする時間を示します。

次の手順に従います。

1.  ターゲット コンピューターのレジストリに次のように設定します。 **HostProcessDbgBreakOnStart**または**HostProcessDbgBreakOnDriverLoad**秒と再起動のいくつかの数。
2.  対象のコンピューターに管理者として、WinDbg を開きます。
3.  **ファイル**] メニューの [選択**プロセスにアタッチ**します。 選択**実行可能ファイルによって**WUDFHost.exe (できない可能性がありますいずれか) という名前のすべてのプロセスを見つけます。 WUDFHost.exe という名前のプロセスがある場合は、今後の参照用のプロセス id を書き留めます。
4.  デバイス マネージャーでは、ドライバーを有効にします。
5.  手順 2 を繰り返し、WUDFHost.exe の新しいインスタンスを検索します。 WUDFHost.exe の新しいインスタンスが表示されない場合はクリックして**キャンセル**、選択**プロセスにアタッチ**もう一度です。 WUDFHost.exe の新しいインスタンスを検索するときに選択し、をクリックして**OK**します。

場合[デバイス プール](using-device-pooling-in-umdf-drivers.md)はセット内に使用して、 **HostProcessDbgBreakOnDriverLoad**レジストリ値、その他のドライバーの読み込み中にデバッガーを中断表示可能性があります。 UMDF デバッグ モードを使用してデバイスのプールを無効にすることができます。

デバッグ モードを使用する、Visual Studio で f5 キーを押してオプションを使用するか設定、 **DebugModeFlags**と**DebugModeBinaries**レジストリの値。

UMDF レジストリ値の詳細については、[デバッグの WDF ドライバー (KMDF および UMDF) のレジストリ値](registry-values-for-debugging-kmdf-drivers.md)を参照してください。

## <a href="" id="kd"></a>WinDbg を使用して (カーネル モードのデバッグ) ホスト コンピューターからリモートでデバッグするには


リモート ホストからカーネル モードのデバッグ セッションを確立し、ドライバーをホストしている Wudfhost のインスタンスに現在のプロセスを設定します。 リモート カーネル デバッガーからデバッグする場合は設定できます**HostProcessDbgBreakOnDriverStart**または**HostProcessDbgBreakOnDriverLoad** 0x80000000 のタイムアウトを指定しないが、カーネルに分割するにはデバッガー。

UMDF 1.11 以降では、カーネル デバッガーを分割する前に、reflector は自動的に切り替わりますプロセスのコンテキストのホスト プロセス。 最初に発行することがなく UMDF デバッガー拡張機能のコマンドをすぐに使用する結果として、 [ **.process** ](https://msdn.microsoft.com/library/windows/hardware/ff564723)プロセスのコンテキストを変更するコマンド。

これらの手順に従います。

1. プールを無効にします。 オンにする**DebugModeFlags**一覧で、ドライバーと**DebugModeBinaries**
2. ドライバーは、UMDF 1.11 以降を使用している場合**HostFailKdDebugBreak**既定で有効です。 この手順をスキップします。

   ドライバーは、UMDF 1.9 またはそれ以前を使用している場合は、設定**HostFailKdDebugBreak**を 1 にします。

3. タイムアウトに関連する問題をデバッグする場合は、オフにする**HostProcessDbgBreakOnDriverStart**と**HostProcessDbgBreakOnDriverLoad**します。 (と**HostProcessDbgBreakOnDriverStart**または**HostProcessDbgBreakOnDriverLoad** 0 以外の場合は、フレームワーク、reflector は、ユーザー モード中にホストを終了しないように、タイムアウトを無効にします。デバッガーがアタッチされているホスト プロセスにします。)これら 2 つの値を使用する代わりに、ドライバーの初期化コードをデバッグする必要がある場合、ドライバーの読み込み前に、WinDbg で次のコマンドの発行を再試行してください: **sxe ld:**<em>MyDriver.dll</em> (モジュールの読み込み時に中断)
4. レジストリの変更を加えた場合に再起動します。
5. 上記で作成した、選択に応じてドライバーをロードまたはアンロード、ターゲットの場合、リモートのカーネル デバッガーを中断します。

 

 





