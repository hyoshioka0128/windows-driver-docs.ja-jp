---
title: UMDF ドライバーのデバッグを有効にする方法
description: UMDF ドライバーのデバッグを有効にする方法
ms.assetid: ea37eb7b-09fa-4c8d-aff7-273b07bc0007
keywords:
- デバッガー WDK UMDF
- デバッガー WDK UMDF、有効化
- ユーザーモードドライバーフレームワーク WDK、デバッガーの有効化
- UMDF WDK、デバッガーの有効化
- ユーザーモードドライバー WDK UMDF、デバッガーの有効化
- ドライバーのデバッグ WDK UMDF、デバッガーの有効化
- ドライバーのデバッグ WDK UMDF、デバッガーの有効化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ab2ac66d915d8ff16975a979cfd09363648b44f
ms.sourcegitcommit: 7dff2005387294dbfeeec45c801bf6b4a4cb9319
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2020
ms.locfileid: "80261282"
---
# <a name="how-to-enable-debugging-of-a-umdf-driver"></a>UMDF ドライバーのデバッグを有効にする方法


開発中にユーザーモードドライバーフレームワーク (UMDF) ドライバーをデバッグするには、次の構成を使用します。 すべての構成には、ホストとターゲットという2台のコンピューターが含まれます。 

-   ドライバーをターゲットに手動でコピーします。 ターゲットでユーザーモードのデバッグを実行します。 このシナリオでは、ターゲットで実行されているドライバーホストプロセスのインスタンスに手動で接続します。
-   ドライバーをターゲットに手動でコピーし、ホストからカーネルモードのデバッグを実行します。

カーネルデバッガーをアタッチして、すべての UMDF ドライバーのテストと開発を行うことをお勧めします。

## <a name="best-practices"></a><a href="" id="bp"></a>ベストプラクティス

カーネルデバッガーをアタッチして、すべての UMDF ドライバーテストを実行することをお勧めします。

推奨される設定は次のとおりです。 これらの設定を手動で設定することも、WDK の[WDF Verifier コントロールアプリケーション](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdf-verifier-control-application)(wdfverifier) ツールを使用してこれらの設定を表示または変更することもできます。

-   WUDFHost .exe でアプリケーション検証ツールを有効にします。

    ```cpp
    AppVerif –enable Heaps Exceptions Handles Locks Memory TLS Leak –for WudfHost.exe
    ```

    例外が発生した場合、アプリケーション検証ツールによってデバッガーに診断メッセージが送信され、が中断されます。

-   カーネルモードのデバッグセッションを使用している場合は、ドライバーホストプロセスを終了する前に、 **HostFailKdDebugBreak**を設定して、リフレクターがカーネルモードのデバッガーを中断するようにします。 Windows 8 以降では、この設定は既定で有効になっています。

-   **Umdfhostprocesssharing**を**processsharingdisabled**に設定して、プーリングを無効にします。 詳細については、「 [INF ファイルでの WDF ディレクティブの指定](specifying-wdf-directives-in-inf-files.md)」を参照してください。
-   既定では、UMDF デバイスで障害が発生すると、フレームワークは最大5回、再起動を試みます。 自動再起動を無効にするには、 **DebugModeFlags**を0x01 に設定します。 詳細については、「 [WDF Drivers をデバッグするためのレジストリ値](registry-values-for-debugging-kmdf-drivers.md)」を参照してください。
-   コンピューターを再起動します。

-   UMDF ドライバーの問題のデバッグについて[は、リフレクタがホストプロセスを終了](determining-why-the-reflector-terminated-the-host-process.md)し、 [UMDF ドライバーのクラッシュをデバッグ](debugging-umdf-2-0-drivers.md)する理由の確認 

## <a name="using-windbg-to-attach-manually-user-mode-debugging"></a>WinDbg を使用して手動でアタッチする (ユーザーモードのデバッグ)


ターゲットコンピューターでは、そのドライバーをホストする WUDFHost のインスタンスに対して、手動で WinDbg をアタッチできます。 アタッチすると、デバッガーが中断され、ドライバーにブレークポイントを設定できます。

ドライバーの初期化は、WUDFHost が読み込まれた直後に発生するため、手動でアタッチして初期化コードをデバッグすることはできません。 代わりに、ホストの初期化時またはドライバーの読み込み時に、ホストプロセスが数秒間待機するようにレジストリ値を設定できます。 この遅延により、WinDbg を WUDFHost プロセスの正しいインスタンスにアタッチする時間が与えられます。

次の手順に従います。

1.  ターゲットコンピューターのレジストリで、 **Hostprocessdbgbreakonstart**または**Hostprocessdbgbreakondriverload**をいくつかの秒数に設定し、再起動します。
2.  ターゲットコンピューターで、[管理者として WinDbg] を開きます。
3.  **[ファイル]** メニューの **[プロセスにアタッチ]** をクリックします。 **[実行可能ファイル]** を選択し、WUDFHost .exe という名前のすべてのプロセスを検索します (存在しない可能性があります)。 WUDFHost .exe という名前のプロセスがある場合は、後で参照できるようにプロセスの識別子を書き留めておきます。
4.  デバイスマネージャーで、ドライバーを有効にします。
5.  手順2を繰り返し、WUDFHost の新しいインスタンスを見つけます。 WUDFHost .exe の新しいインスタンスが表示されない場合は、 **[キャンセル]** をクリックし、 **[プロセスにアタッチ]** をもう一度クリックします。 WUDFHost .exe の新しいインスタンスを見つけたら、それを選択し、 **[OK]** をクリックします。

[デバイスプール](using-device-pooling-in-umdf-drivers.md)が使用されていて、 **Hostprocessdbgbreakondriverload**レジストリ値を設定している場合は、他のドライバーの読み込みによってデバッガーが中断する可能性があります。 UMDF デバッグモードを使用して、デバイスプールを無効にすることができます。

デバッグモードを使用するには、Visual Studio で F5 オプションを使用するか、レジストリで**DebugModeFlags**と**Debugmodebinaries バイナリ**値を設定します。

UMDF レジストリ値の詳細については、「 [WDF Drivers (KMDF および UMDF) をデバッグするためのレジストリ値](registry-values-for-debugging-kmdf-drivers.md)」を参照してください。

## <a name="using-windbg-to-remotely-debug-from-a-host-machine-kernel-mode-debugging"></a><a href="" id="kd"></a>WinDbg を使用したホストコンピューターからのリモートデバッグ (カーネルモードデバッグ)


リモートホストからカーネルモードのデバッグセッションを確立し、現在のプロセスを、ドライバーをホストしている Wudfhost のインスタンスに設定します。 リモートカーネルデバッガーからデバッグしている場合は、 **Hostprocessdbgbreakondriverstart**または**Hostprocessdbgbreakondriverstart**を0x80000000 に設定してタイムアウトを指定せずに、カーネルデバッガーを中断することができます。

次の手順を使用します。

1. プーリングを無効にします。 **DebugModeFlags**を有効にし、 **debugmodebinaries**でドライバーを一覧表示する
2. ドライバーで UMDF 1.11 以降が使用されている場合、 **HostFailKdDebugBreak**は既定で有効になっています。 この手順をスキップします。

   ドライバーで UMDF 1.9 以前を使用している場合は、 **HostFailKdDebugBreak**を1に設定します。

3. タイムアウトに関連する問題をデバッグしている場合は、 **Hostprocessdbgbreakondriverstart**と**Hostprocessdbgbreakondriverstart**をオフにします。 ( **Hostprocessdbgbreakondriverstart**または**Hostprocessdbgbreakondriverstart**が0以外の場合、フレームワークはタイムアウトを無効にして、ユーザーモードのデバッガーがホストプロセスにアタッチされている間にリフレクターがホストを終了しないようにします。)ドライバー初期化コードをデバッグする必要がある場合は、これら2つの値を使用する代わりに、次のコマンドを WinDbg で発行してみてください: **sxe ld:** <em>mydriver .dll</em> (モジュールの負荷で中断)
4. レジストリを変更した場合は、再起動します。
5. 上で選択した内容に応じて、リモートカーネルデバッガーは、ターゲットでドライバーが読み込まれるかアンロードされるときに中断されます。

 

 





