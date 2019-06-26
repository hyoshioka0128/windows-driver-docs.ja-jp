---
title: フレームワークのイベント ロガーの使用
description: フレームワークのイベント ロガーの使用
ms.assetid: aa0a83c8-cd13-41d0-a619-d8793b2e2e80
keywords:
- ドライバー WDK KMDF、イベント ログ機能のデバッグ
- イベント ロガー WDK KMDF
- 実行中のレコーダー WDK KMDF
- IFR WDK KMDF
- イベント ログの WDK KMDF
- WDK KMDF のエラー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be056678c094610458c2465592023eaa3e599f16
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372208"
---
# <a name="using-the-frameworks-event-logger"></a>フレームワークのイベント ロガーの使用


WDF にはフレームワークとも呼ばれる、内部トレース ロガーが含まれています*インフライト レコーダー* (IFR)。 WDF のロガーは、WDF ドライバーごとにイベントの最新の履歴を含むトレース ログを作成します。 トレース ログは、フレームワークと、対応する要求のドライバーを介して、I/O 要求パケット (Irp) の進行状況を追跡します。 各カーネル モード ドライバー フレームワーク (KMDF) とユーザー モード ドライバー フレームワーク (UMDF) ドライバーでは、独自のログがあります。

WDF の logger は常に有効にします。 各トレース ログのロガーは循環メモリ バッファーにイベント レコードを格納します。 必要に応じて、詳細レコードへのエントリなど、ドライバーをデバッグするのに役立つ追加情報をイベント ロガーまたは内部のコード パスからの終了が上にできます。 既定では、バッファーのサイズが 1 つのメモリ ページと詳細度は無効になります。 内でこれらの値を調整することで、バッファーのサイズと詳細度を変更することができます、 [WdfVerifier アプリケーション](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdf-verifier-control-application)します。 詳細度の有効化とシステム パフォーマンスが低下ことに注意してください。

WDF デバッガー拡張機能を使用するには表示および対話形式デバッグ中には、WDF のログを保存します。 デバッグ セッション中に WDF ログを表示します。

1.  適切なシンボルを読み込みます。 使用することができます、 [ **.symfix**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-symfix--set-symbol-store-path-)+ デバッガー コマンドを既存のシンボル パスに、Microsoft パブリック シンボル ストアを追加します。 パブリック シンボル ストアには、WDF バイナリのシンボルが含まれています。 また、ドライバーのシンボルのシンボルを読み込む可能性があります。

    取得する方法に関する追加情報 ウィンドウのシンボルと、デバッガーのシンボル パスを設定する方法を参照してくださいで提供されるドキュメント、 [Windows デバッグ](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)パッケージ。

2.  ロード、 [Wdfkd.dll 拡張機能ライブラリ](debugger-extensions-for-kmdf-drivers.md)デバッガーを起動します。 カーネル デバッガーを使用している場合は、これを行うを使用して、 [ **.load** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-load---loadby--load-extension-dll-)コマンド。 Wdfkd.dll の正しいバージョンを読み込むには、DLL の完全修飾パスを指定する必要があります。 たとえばには、次のパスは、デバッガーの x86 ベースのホスト コンピューター上に使用します。

    ```cpp
    .load "C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\winext\wdfkd.dll"
    ```

    使用して、拡張機能が読み込まれているを確認することができますし、 [ **! チェーン**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-chain--list-debugger-extensions-)読み込まれたすべての拡張機能を表示するコマンド。

    Framework デバッガー拡張機能の詳細については、使用、 [ **! wdfhelp** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfhelp)拡張機能。 カーネル デバッガーの詳細についてで提供されるドキュメントを参照して、 [Windows デバッグ](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)パッケージ。

3.  フレームワークのバージョン 1.11 以降を使用するには、ドライバーから Windows 8 またはそれ以降、カーネル デバッガーを使用している場合は、この手順をスキップすることができます。

    ドライバーは、バージョン 1.11 より前のフレームワークを使用している場合を使用して、 [ **! wdftmffile** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdftmffile)または[ **! wdfsearchpath** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfsearchpath)を指定する、プラットフォーム固有のトレース メッセージの形式 (.tmf) ファイル、または .tmf ファイルへのパス。 .Tmf ファイルは、WDK でプラットフォーム固有のサブディレクトリに配置されます。

    .Tmf ファイルは特定のバージョンであるために、現在実行されているフレームワークのランタイム ライブラリのバージョンに対応する .tmf ファイルを指定する必要があります。 たとえば、KMDF バージョン 1.9 がホスト マシンで実行されているとします。

    ```cpp
    !wdftmffile c:\WinDDK\<version>\tools\tracing\x86\wdf01009.tmf
    ```

    トレースを設定して、検索パスを設定することもできます。\_形式\_検索\_PATH 環境変数。 [ **! Wdftmffile** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdftmffile)コマンド検索パス環境変数で設定されているよりも優先されます。

    Framework のバージョン番号を確認するには実行、 [ **! wdfldr** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfldr)デバッガー カーネル デバッガーから拡張機能コマンド。

4.  使用して、 [ **! wdflogdump** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdflogdump)イベント ロガーのレコードを表示する拡張機能。 たとえば、WinDbg コマンド ウィンドウの次のスクリーン ショットは出力の典型的な例を示しています **! wdflogdump**:。

    ![サンプルからの出力、! wdflogdump 拡張機能](images/kmdf-using-wdflogdump.png)

フレームワークのログ内の各行は前に呼び出される文字列、[トレース メッセージのプレフィックス](https://docs.microsoft.com/windows-hardware/drivers/devtest/trace-message-prefix)します。 トレース ロガーは、ログに書き込まれた各メッセージには、このプレフィックスを付加します。 既定では、プレフィックスには、データ要素の標準セットが含まれていますが、特定の要件に合わせて既定の要素を変更することができます。 WDF のドライバーのプレフィックス文字列を変更するには、トレースを設定して\_形式\_プレフィックス環境変数またはを使用して、 [ **! wdfsettraceprefix** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfsettraceprefix)デバッガー拡張機能コマンド。

環境変数を設定するには、次のようなコマンドを使用します。

```cpp
Set TRACE_FORMAT_PREFIX=%2!s!: %!FUNC!: %8!04x!.%3!04x!: %4!s!:
```

このコマンドでは、次に、トレース メッセージのプレフィックスを設定します。

```cpp
SourceFile_LineNumber: FunctionName: ProcessID.ThreadID: SystemTime
```

使用することも、 [ **! wdflogsave** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdflogsave)拡張機能コマンドで、イベント トレース ログ (.etl) ファイルを使用して表示できるイベント ロガーのレコードを保存する[traceview で](https://docs.microsoft.com/windows-hardware/drivers/devtest/traceview)します。

使用することができる場合があります、 [ **! wdfcrashdump** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfcrashdump)デバッガーのシステムのバグを確認した後、ログ情報を表示するクラッシュ ダンプで拡張機能。 ログ情報が使用可能なクラッシュ ダンプで、ドライバーにバグ チェックが発生したことか、設定したかどうか、フレームワークを調べる場合にのみ、 [ForceLogsInMiniDump](registry-values-for-debugging-kmdf-drivers.md)ドライバーのレジストリ値。

使用するかバグ チェックが発生した場合、デバッガーが接続されている場合は[ **! wdfcrashdump** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfcrashdump)ログを表示するかについては、すぐに情報を表示できます、メモリ ダンプ ファイルを読み込むことで。 小さいメモリ ダンプ ファイルのサイズの制限により、ログ、クラッシュの原因となったドライバーを可能性があります、ダンプには表示されません。

フレームワークは、特定のドライバーの原因か次のバグ チェックのコードを特定できます。

-   [**バグ チェック 0xD1 の。ドライバー\_IRQL\_いない\_少ない\_または\_と等しい**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xd1--driver-irql-not-less-or-equal)
-   [**0 xa-チェックをバグします。IRQL\_いない\_少ない\_または\_と等しい**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xa--irql-not-less-or-equal)
-   [**バグの 0x20 をチェックします。カーネル\_APC\_PENDING\_に\_終了**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0x20--kernel-apc-pending-during-exit)
-   [**バグ チェック 0x8E の。カーネル\_モード\_例外\_いない\_処理済み**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0x8e--kernel-mode-exception-not-handled)
-   [**バグ チェック 0x1E の。KMODE\_例外\_いない\_処理済み**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0x1e--kmode-exception-not-handled)
-   [**バグのチェック 0x50 です。ページ\_フォールト\_IN\_非ページ\_領域**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0x50--page-fault-in-nonpaged-area)
-   [**バグ チェック 0x7E の。システム\_スレッド\_例外\_いない\_処理済み**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0x7e--system-thread-exception-not-handled)

UMDF 以降 UMDF バージョン 2 では、UMDF のトレース ログを保存 (または UMDF *IFR*) 非ページ メモリのカーネルにします。 フレームワークは、ドライバーのホスト (Wudfhost) インスタンスごとの 1 つの IFR を割り当てます。

デバッガーの拡張機能コマンドの詳細については、次を参照してください。 [Framework ベースのドライバーの拡張機能をデバッガー](debugger-extensions-for-kmdf-drivers.md)します。

 

 





