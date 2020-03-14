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
ms.openlocfilehash: afaf1f6e452ecbf784907f87842f6ee64b2e0aac
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242889"
---
# <a name="how-to-enable-debugging-of-a-umdf-driver"></a>UMDF ドライバーのデバッグを有効にする方法


次の構成を使用して、ユーザーモードドライバーフレームワーク (UMDF) ドライバーをデバッグできます。 すべての構成には、ホストとターゲットという2台のコンピューターが含まれます。 Microsoft Visual Studio と Windows Driver Kit (WDK) を実行して、ホストコンピューターでドライバーを構築し、ターゲットコンピューターにドライバーをインストールしてテストします。

-   Visual Studio を使用してドライバーをターゲットにコピー ("配置") し、ホスト上の Visual Studio 内でユーザーモードのデバッグセッションを開始します。
-   ドライバーをターゲットに手動でコピーします。 ターゲットでユーザーモードのデバッグを実行します。 このシナリオでは、ターゲットで実行されているドライバーホストプロセスのインスタンスに手動で接続します。
-   ドライバーをターゲットに手動でコピーし、ホストからカーネルモードのデバッグを実行します。

後者の2つの構成を一緒に使用して、ターゲットでのユーザーモードのデバッガーとホスト上のカーネルモードのデバッガーの両方を実行できます。

## <a href="" id="bp"></a>ベストプラクティス


カーネルデバッガーをアタッチして、すべての UMDF ドライバーテストを実行することをお勧めします。

推奨される設定は次のとおりです。 これらの設定を手動で設定することも、WDK の[WDF Verifier コントロールアプリケーション](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdf-verifier-control-application)(wdfverifier) ツールを使用してこれらの設定を表示または変更することもできます。

-   WUDFHost .exe でアプリケーション検証ツールを有効にします。

    ```cpp
    AppVerif –enable Heaps Exceptions Handles Locks Memory TLS Leak –for WudfHost.exe
    ```

    例外が発生した場合、アプリケーション検証ツールによってデバッガーに診断メッセージが送信され、が中断されます。

-   [ドライバーの検証](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)を有効にします。 **コマンドプロンプト**ウィンドウを開きます ( **[管理者として実行]** )。 「Verifier」と入力して、Driver Verifier マネージャーを開きます。
-   カーネルモードのデバッグセッションを使用している場合は、ドライバーホストプロセスを終了する前に、 **HostFailKdDebugBreak**を設定して、リフレクターがカーネルモードのデバッガーを中断するようにします。 この設定は、既定では、UMDF バージョン1.11 以降で有効になっています。

-   **Umdfhostprocesssharing**を**processsharingdisabled**に設定して、プーリングを無効にします。 詳細については、「 [INF ファイルでの WDF ディレクティブの指定](specifying-wdf-directives-in-inf-files.md)」を参照してください。
-   既定では、UMDF デバイスで障害が発生すると、フレームワークは最大5回、再起動を試みます。 自動再起動を無効にするには、 **DebugModeFlags**を0x01 に設定します。 詳細については、「 [WDF Drivers をデバッグするためのレジストリ値](registry-values-for-debugging-kmdf-drivers.md)」を参照してください。
-   コンピューターを再起動します。

## <a name="using-visual-studio-with-f5-to-attach-automatically-user-mode-debugging"></a>F5 キーを押して Visual Studio を使用して自動的にアタッチする (ユーザーモードのデバッグ)


WDK と共に Visual Studio を使用してテストコンピューターのドライバーをデバッグするには、まずテストコンピューターをセットアップして構成する必要があります。 これを行う方法については、「[テストコンピューターへのドライバーの展開](https://docs.microsoft.com/windows-hardware/drivers)」を参照してください。

テストコンピューターを構成したら、ホストコンピューターで Visual Studio を使用して、ドライバーにブレークポイントを設定します。 F5 キーを押すと、Visual Studio によってドライバーがビルドされ、対象のコンピューターに配置され、ユーザーモードのデバッグセッションが開始されます。

この手法を使用して UMDF ドライバーを配置すると、Visual Studio によってそのドライバーの*umdf デバッグモード*が有効になります。 既定では、デバッグモードは次のことを意味します。

-   ドライバーは、独自の専用ホストプロセスで開始されます。 [デバイスプーリング](using-device-pooling-in-umdf-drivers.md)はオフになっています。
-   ドライバーがクラッシュした後、デバイスは自動的に再起動されず、エラー報告は無効になります。
-   フレームワークは、「 [UMDF でのホストプロセスタイムアウト](how-umdf-enforces-time-outs.md)」で説明されているタイムアウトを適用しません。
-   UMDF ホストプロセスまたはフレームワーク検証ツールによって無効な操作が検出された場合、UMDF はユーザーモードのデバッガーに中断します。

ドライバーのインストールに再起動が必要な場合でも、デバッグモードを使用して、UMDF ドライバーをデバッグできます。 ユーザーがログインする前に開始されるユーザーモードドライバー (生体認証、スマートカード、入力など) をデバッグすることもできます。

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

## <a href="" id="kd"></a>WinDbg を使用したホストコンピューターからのリモートデバッグ (カーネルモードデバッグ)


リモートホストからカーネルモードのデバッグセッションを確立し、現在のプロセスを、ドライバーをホストしている Wudfhost のインスタンスに設定します。 リモートカーネルデバッガーからデバッグしている場合は、 **Hostprocessdbgbreakondriverstart**または**Hostprocessdbgbreakondriverstart**を0x80000000 に設定してタイムアウトを指定せずに、カーネルデバッガーを中断することができます。

UMDF 1.11 以降では、カーネルデバッガーを中断する前に、リフレクターはプロセスコンテキストをホストプロセスのコンテキストに自動的に切り替えます。 その結果、最初に. process コマンドを発行してプロセスコンテキストを変更しなくても、UMDF デバッガー拡張コマンドをすぐに使用でき[**ます。** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-process--set-process-context-)

次の手順を使用します。

1. プーリングを無効にします。 **DebugModeFlags**を有効にし、 **debugmodebinaries**でドライバーを一覧表示する
2. ドライバーで UMDF 1.11 以降が使用されている場合、 **HostFailKdDebugBreak**は既定で有効になっています。 この手順をスキップします。

   ドライバーで UMDF 1.9 以前を使用している場合は、 **HostFailKdDebugBreak**を1に設定します。

3. タイムアウトに関連する問題をデバッグしている場合は、 **Hostprocessdbgbreakondriverstart**と**Hostprocessdbgbreakondriverstart**をオフにします。 ( **Hostprocessdbgbreakondriverstart**または**Hostprocessdbgbreakondriverstart**が0以外の場合、フレームワークはタイムアウトを無効にして、ユーザーモードのデバッガーがホストプロセスにアタッチされている間にリフレクターがホストを終了しないようにします。)ドライバー初期化コードをデバッグする必要がある場合は、これら2つの値を使用する代わりに、次のコマンドを WinDbg で発行してみてください: **sxe ld:** <em>mydriver .dll</em> (モジュールの負荷で中断)
4. レジストリを変更した場合は、再起動します。
5. 上で選択した内容に応じて、リモートカーネルデバッガーは、ターゲットでドライバーが読み込まれるかアンロードされるときに中断されます。

 

 





