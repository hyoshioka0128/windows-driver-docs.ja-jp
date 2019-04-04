---
title: WDF の Windows パフォーマンス ツールキット (WPT) を使用します。
description: Windows 10 以降、Windows パフォーマンス ツールキット (WPT) を使用して、KMDF または 2 の UMDF ドライバーのパフォーマンス データを表示します。
Search.SourceType: Video
ms.assetid: 0442E4E2-DBC7-4EB0-BEB6-49EFF5132A1D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e4cbfe2e61cbc474055f06e9e73f7a417a18b69
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557302"
---
# <a name="using-the-windows-performance-toolkit-wpt-with-wdf"></a>WDF の Windows パフォーマンス ツールキット (WPT) を使用します。


Windows 10 以降、Windows パフォーマンス ツールキット (WPT) を使用して、指定されたカーネル モード ドライバー フレームワーク (KMDF) またはユーザー モード ドライバー フレームワーク (UMDF) 2 のドライバーのパフォーマンス データを表示します。

## <a name="how-can-the-windows-driver-frameworks-wdf-extensions-for-wpt-help"></a>WPT の Windows Driver Frameworks (WDF) 拡張機能はどのように役立つことができますか


WPT を使用して、パフォーマンスの洞察を取得またはパフォーマンスの問題のトラブルシューティングを行うことができます。 次に、例を示します。

-   ドライバーの WDF の I/O 要求の完了率、CPU 使用率、および PnP と電力のコールバックに費やされた時間を確認します。
-   ような KMDF ドライバーに対して 2 の UMDF ドライバーを比較し、UMDF が、パフォーマンスの要件を満たしているかどうかを判断します。
-   WDF の I/O パスでパフォーマンスの問題を特定します。
-   指定されたコールバックのインスタンスには、長い時間がかかるかを決定します。 理由を理解するサンプリングの CPU 使用率を調べる。
-   かどうか、デバイスは行って power 遷移 D0 電源の状態との間あまり頻繁に確認してください。

## <a name="getting-started"></a>概要


WPT は、Windows アセスメント & デプロイメント キット (ADK) の一部です。 ADK をインストールすることができます、 [Windows ハードウェア ツール](http://dev.windows.com/featured/hardware/windows-10-hardware-preview-tools)サイト。

WPT は、2 つの独立したツールで構成されます。Windows パフォーマンス レコーダーと Windows パフォーマンス アナライザー (WPA)。 このトピックでは、トレース、および、構成可能な GUI 形式で、トレースを表示するのに WPA を記録するのに WPR を使用します。

Windows パフォーマンス ツールキットを使用して、WDF ドライバーのパフォーマンスを測定する方法については、次のビデオを見るか、またはビデオ以下の手順を読み取る。 ビデオと手順は、同じ手順をについて説明します。
>[!VIDEO https://www.microsoft.com/videoplayer/embed/fc37f465-9456-45d7-bbe9-6f7d44342563]

**記録と WDF ドライバーのイベント ログの表示**

1.  まだインストールされていない場合、ドライバーをインストールします。

2.  管理者特権でコマンド プロンプトで、次のコマンドを入力します。

    **WdfPerfEnhancedVerifier.cmd**  *&lt;ServiceName&gt;&lt;UMDF または KMDF&gt;*

    **注**WdfPerfEnhancedVerifier.cmd をコピーする必要があります WPT をインストールした場所からします。 WPT を開発用コンピューターにインストールした場合は、ターゲット コンピューターに WPT のインストール ディレクトリからスクリプトをコピーする必要があります。




このスクリプトでは、フレームワークは、手順 4. で ETW プロバイダーが有効にすると、パフォーマンスの分析を有効にするために必要なイベントを記録するために、指定されたドライバーのレジストリ エントリを設定します。


3.  コンピューターを再起動します。
4.  管理者特権でコマンド プロンプトで、次のコマンドを入力します。

    **Wpr.exe** **-Start WdfPerfTraceProviders.wprp**

    このコマンドは、WDF の ETW プロバイダーを使用できます。 コンピューターでは、トレースの記録を開始します。

    **注**WPT がインストールされているように手順 2. で Wpr.exe および WdfPerfTraceProviders.wprp を場所からコピーする必要があります。 WPT を開発用コンピューターにインストールした場合は、ターゲット マシンに WPT のインストール ディレクトリからこれらのファイルをコピーします。




Windows 10 デスクトップ エディション (Home、Pro、Enterprise、および教育機関向け) の場合、Wprui.exe、トレースを記録するための GUI を提供すると、トレースを開始することもできます。


5.  関心のあるシナリオを実行します。
6.  ETW トレース セッションを停止します。**Wpr.exe -Stop MyPerfTrace.etl**
7.  Windows Performance Analyzer ビューアーでイベントのトレース ログを開きます。

    **Wpa.exe MyPerfTrace.etl**

同じドライバーを別のトレースをキャプチャするには、Wpr.exe を使用して起動し、新しいトレースを停止します。 別のドライバーのトレースをキャプチャするには、まず、新しいドライバーの WdfPerfEnhancedVerifier.cmd を再実行します。

## <a name="analyzing-the-trace"></a>トレースの分析


ドライバーのパフォーマンスの分析を開始するには、検索、 **Graph Explorer**左側で、開く、**計算**カテゴリ、および UMDF または KMDF の下のメイン作業領域にグラフをドラッグ、 **分析**タブ。このスクリーン ショットは、 **Graph Explorer**ウィンドウ。

![wpa で graph エクスプ ローラー](images/WpaUMDFIoCapture-LeftPane.png)

UMDF および KMDF ドライバー用に別の専用のテーブルがあります。

## <a name="umdf-io-request-graph-and-summary-table"></a>UMDF I/O 要求のグラフや概要テーブル


WPT は、2 つの方法で、WDF の I/O 要求の完了のスループットを表示できます。

-   1 秒あたりの完了の I/O 要求の数
-   (ガント チャートとして書式設定) の I/O 要求ごとの時間の期間

次のスクリーン ショットは、サンプルの概要グラフとテーブル CPU および UMDF I/O 要求のパフォーマンスを示しています。 UMDF I/O 要求の処理の完了率のグラフでは、1 秒あたりの要求の数が y 軸に表示されます。

![umdf i/o 要求のパフォーマンスのグラフ](images/WpaUMDFIoCapture-Narrow.PNG)

[概要テーブル](https://msdn.microsoft.com/library/windows/hardware/hh448109.aspx)、ほとんどの列は文字どおりがある点に注意してください。 WdfDevice 列には、I/O 要求に関連付けられた WDFDEVICE ハンドルが含まれています。 ActivityID には、I/O 要求の一意の識別子が含まれています。 フレームワークは、I/O 要求をドライバーに配信するときに、この識別子を作成します。 アクティビティの識別子が既に対応する IRP に関連付けられている場合、フレームワークは、その識別子を使用します。 詳細については、[アクティビティ識別子を使用して](using-activity-identifiers.md)を参照してください。

フレームワークは、ドライバーに要求を配信し、ドライバーが呼び出されたときに、終了時刻は、タイムスタンプ、エントリの時刻がトレース タイムスタンプ[ **WdfRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff549945)または完了に関連するメソッド、要求。

## <a name="kmdf-io-request-graph-and-summary-table"></a>KMDF I/O 要求のグラフや概要テーブル


KMDF ドライバーの I/O 要求の情報を示すようなスクリーン ショットを次に示します。

![umdf i/o 要求のパフォーマンスのグラフ](images/WpaKMDFIoCapture-Narrow.PNG)

## <a name="pnp-power-callback-graph-and-summary-table"></a>PnP Power コールバックのグラフや概要テーブル


WPT では、各 PnP と電力のコールバックの処理時間も表示できます。 次のスクリーン ショット[ *EvtDeviceD0Entry*](https://msdn.microsoft.com/library/windows/hardware/ff540848)、 [ *EvtDeviceD0Exit* ](https://msdn.microsoft.com/library/windows/hardware/ff540855)と[ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)サンプル KMDF ドライバーおよび UMDF ドライバーのサンプルのコールバックの実行時間。

WdfDevice 列には、コールバックに関連付けられた WDFDEVICE ハンドルが含まれています。 ActivityID には、コールバック インスタンスの一意の識別子が含まれています。

![pnp power callback graph](images/wpa-fx2-pnppwr.PNG)

## <a name="which-calls-are-instrumented"></a>どの呼び出しがインストルメント化しますか。


このセクションでは、グラフとテーブルの上に示したの構築に使用するイベントについて説明します。

システムがいくつかの指定したドライバーのコールバック関数を呼び出すときに、フレームワークが ETL トレース ログにイベントを記録 WdfPerfEnhancedVerifier.cmd の特定のドライバーを実行した後、指定したドライバーがいくつかのフレームワーク メソッドを呼び出すときにもとします。

判断するには、I/O 要求開始と、次のコールバックを呼び出すときに、フレームワークのレコード イベント。

-   [*EvtIoDefault*](https://msdn.microsoft.com/library/windows/hardware/ff541757)
-   [*EvtIoRead*](https://msdn.microsoft.com/library/windows/hardware/ff541776)
-   [*EvtIoWrite*](https://msdn.microsoft.com/library/windows/hardware/ff541813)
-   [*EvtIoDeviceControl*](https://msdn.microsoft.com/library/windows/hardware/ff541758)
-   [*EvtIoInternalDeviceControl*](https://msdn.microsoft.com/library/windows/hardware/ff541768)

フレームワークでは、ドライバーは、次のメソッドを呼び出すときに、I/O 要求開始イベントも記録します。

-   [**WdfIoQueueRetrieveNextRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548462)
-   [**WdfIoQueueRetrieveRequestByFileObject**](https://msdn.microsoft.com/library/windows/hardware/ff548470)
-   [**WdfIoQueueRetrieveFoundRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548456)

I/O 要求完了したときを確認するのには、フレームワークは、ドライバーを呼び出すときを追跡します。

-   [**WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945)
-   [**WdfRequestCompleteWithInformation**](https://msdn.microsoft.com/library/windows/hardware/ff549948)
-   [**WdfRequestCompleteWithPriorityBoost**](https://msdn.microsoft.com/library/windows/hardware/ff549949)

最後に、PnP/電源コールバックのコールバックの実行時間を決定するフレームワークとを記録、次のドライバーが提供するコールバック ルーチンの呼び出し時に、[完了]。

-   [*EvtDeviceD0Entry*](https://msdn.microsoft.com/library/windows/hardware/ff540848)
-   [*EvtDeviceD0Exit*](https://msdn.microsoft.com/library/windows/hardware/ff540855)
-   [*EvtDevicePrepareHardware*](https://msdn.microsoft.com/library/windows/hardware/ff540880)
-   [*EvtDeviceReleaseHardware*](https://msdn.microsoft.com/library/windows/hardware/ff540890)
-   [*EvtIoStop*](https://msdn.microsoft.com/library/windows/hardware/ff541788)

## <a name="resources-and-troubleshooting"></a>リソースとトラブルシューティング


-   必ず WdfPerfEnhancedVerifier.cmd スクリプトを実行した後に再起動してください。
-   イベント ログを記録するには、ドライバーが構成されているかどうかを調べるには、 **!WdfKd.wdfdriverinfo**カーネル デバッガー コマンド。 ドライバーは、パフォーマンス トレースの構成は、このような出力が表示されます。

    ```cpp
    !WdfKd.WdfDriverInfo Echo.sys
    …
    …
    ----------------------------------

    WDF Verifier settings for echo.sys is ON
      Enhanced verifier: performance analysis hooking ON
    ----------------------------------
    ```

-   開発とテストのみを目的の場合は、ドライバーのコード署名ポリシーの適用を一時的に無効にできます。 詳細については、[開発およびテスト中に、符号なしのドライバー パッケージをインストールする](https://msdn.microsoft.com/library/windows/hardware/ff547565)を参照してください。
-   Windows 10 Mobile でトレースをキャプチャした場合は、ターゲット デバイスから MyPerfTrace.etl を Wpa.exe をされているコンピューターにコピーする必要があります。 使用することができます、 [TShell ツール](https://sysdev.microsoft.com/Hardware/oem/docs/Phone_Testing/TShell)これを行う。

## <a name="related-topics"></a>関連トピック


[Windows パフォーマンス アナライザー](https://msdn.microsoft.com/library/windows/hardware/hh448170.aspx)










