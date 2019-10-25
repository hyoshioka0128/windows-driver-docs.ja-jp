---
title: WDF での Windows Performance Toolkit (WPT) の使用
description: Windows 10 以降では、Windows パフォーマンスツールキット (WPT) を使用して、KMDF または UMDF 2 ドライバーのパフォーマンスデータを表示できます。
Search.SourceType: Video
ms.assetid: 0442E4E2-DBC7-4EB0-BEB6-49EFF5132A1D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dffee9de59ff54b39940ba7e62d4ec54fa96854c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845427"
---
# <a name="using-the-windows-performance-toolkit-wpt-with-wdf"></a>WDF での Windows Performance Toolkit (WPT) の使用


Windows 10 以降では、Windows パフォーマンスツールキット (WPT) を使用して、特定のカーネルモードドライバーフレームワーク (KMDF) またはユーザーモードドライバーフレームワーク (UMDF) 2 ドライバーのパフォーマンスデータを表示できます。

## <a name="how-can-the-windows-driver-frameworks-wdf-extensions-for-wpt-help"></a>WPT の Windows Driver Framework (WDF) 拡張機能はどのように機能しますか。


WPT を使用すると、パフォーマンスに関する洞察を得たり、パフォーマンスの問題をトラブルシューティングしたりすることができます。 次に、例を示します。

-   ドライバーの WDF i/o 要求の完了率、CPU 使用率、および PnP と電源コールバックに費やされた時間を調べます。
-   UMDF 2 ドライバーを同様の KMDF ドライバーと比較し、UMDF がパフォーマンス要件を満たしているかどうかを判断します。
-   WDF i/o パスでパフォーマンスの異常を特定します。
-   指定されたコールバックのどのインスタンスに長い時間がかかっているかを判断します。 次に、サンプリングされた CPU 使用率を調べて、その理由を理解します。
-   デバイスの電源の切り替えが、D0 の電源状態との間で頻繁に行われているかどうかを確認します。

## <a name="getting-started"></a>開始するには


WPT は、Windows アセスメント & amp; デプロイメントキット (ADK) の一部です。 ADK は、 [Windows ハードウェアツール](https://developer.microsoft.com/windows/featured/hardware/windows-10-hardware-preview-tools)のサイトからインストールできます。

WPT は、Windows パフォーマンスレコーダーと Windows パフォーマンスアナライザー (WPA) の2つの異なるツールで構成されています。 このトピックでは、WPR を使用してトレースを記録した後、WPA を使用して、構成可能な GUI 形式でトレースを表示します。

Windows Performance Toolkit を使用して WDF ドライバーのパフォーマンスを測定する方法については、次のビデオを視聴するか、ビデオの以下の手順をお読みください。 ビデオと手順についても同じ手順で説明します。
>[!VIDEO https://www.microsoft.com/videoplayer/embed/fc37f465-9456-45d7-bbe9-6f7d44342563]

**WDF ドライバーのイベントログの記録と表示**

1.  ドライバーがまだインストールされていない場合はインストールします。

2.  管理者特権でのコマンドプロンプトで、次のコマンドを入力します。

    **WdfPerfEnhancedVerifier** *&lt;SERVICENAME&gt;&lt;UMDF または kmdf&gt;*

    **メモ** WdfPerfEnhancedVerifier は、WPT をインストールした場所からコピーする必要があります。 開発用コンピューターに WPT をインストールした場合は、WPT インストールディレクトリからターゲットコンピューターにスクリプトをコピーする必要があります。




このスクリプトは、指定されたドライバーのレジストリエントリを設定します。これにより、手順4で ETW プロバイダーが有効になっている場合に、パフォーマンス分析を有効にするために必要なイベントがフレームワークによってログに記録されます


3.  コンピューターを再起動します。
4.  管理者特権でのコマンドプロンプトで、次のコマンドを入力します。

    **Wpr .exe** **-wdftraceを起動**します。

    このコマンドにより、WDF の ETW プロバイダーが有効になります。 コンピューターがトレースの記録を開始します。

    **注**  手順 2. と同様に、WPT をインストールした場所から wpr をコピーする必要があります。 開発用コンピューターに WPT をインストールした場合は、これらのファイルを WPT インストールディレクトリからターゲットコンピューターにコピーします。

    Windows 10 for desktop edition (Home、Pro、Enterprise、および教育) では、トレースを記録するための GUI を提供する、Wprui でトレースを開始することもできます。 その他のオプション で、**リソース分析** を展開し、**WDF Driver Activity** を選択します。

5.  目的のシナリオを練習します。
6.  ETW トレースセッションを停止する: **Wpr .exe-MyPerfTrace を停止します。**
7.  Windows Performance Analyzer ビューアーでイベントトレースログを開きます。

    **Wpa. .exe MyPerfTrace .etl**

同じドライバーの別のトレースをキャプチャするには、Wpr を使用して新しいトレースを開始および停止します。 別のドライバーのトレースをキャプチャするには、最初に新しいドライバーの WdfPerfEnhancedVerifier を再実行します。

## <a name="analyzing-the-trace"></a>トレースの分析


ドライバーのパフォーマンスの分析を開始するには、左側の**グラフエクスプローラー**を探し、 **[計算]** カテゴリを開いて、 **[分析]** タブの下のメイン作業領域に、UMDF または kmdf グラフをドラッグします。このスクリーンショットは、次の**グラフエクスプローラー**ウィンドウを示しています。

![wpa のグラフエクスプローラー](images/WpaUMDFIoCapture-LeftPane.png)

UMDF 用の専用テーブルと KMDF ドライバー用のテーブルがあります。

## <a name="umdf-io-request-graph-and-summary-table"></a>UMDF i/o 要求グラフと概要テーブル


WPT は、次の2つの方法で WDF i/o 要求の完了スループットを表示できます。

-   1秒間に完了した i/o 要求の数
-   各 i/o 要求の期間 (ガントチャートとして書式設定)

次のスクリーンショットは、CPU および UMDF i/o 要求のパフォーマンスのサンプル概要グラフとテーブルを示しています。 UMDF i/o 要求完了率グラフでは、1秒あたりの要求数が y 軸に表示されます。

![umdf i/o 要求のパフォーマンスのグラフ](images/WpaUMDFIoCapture-Narrow.PNG)

[概要テーブル](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/hh448109(v=win.10))では、ほとんどの列はわかりやすいものですが、注意すべき点がいくつかあります。 WdfDevice 列には、i/o 要求に関連付けられている WDFDEVICE ハンドルが含まれています。 ActivityID には、i/o 要求の一意の識別子が含まれています。 この識別子は、ドライバーに i/o 要求を配信するときに、フレームワークによって作成されます。 アクティビティ識別子が対応する IRP に既に関連付けられている場合、フレームワークはその識別子を使用します。 詳細については、「[アクティビティ識別子の使用](using-activity-identifiers.md)」を参照してください。

Entry time は、フレームワークがドライバーに要求を配信したときのトレースタイムスタンプであり、終了時刻は[**Wdfrequestcomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)を呼び出したときのタイムスタンプ、または要求を完了するための関連メソッドです。

## <a name="kmdf-io-request-graph-and-summary-table"></a>KMDF i/o 要求グラフと概要テーブル


KMDF ドライバーの i/o 要求情報を示す同様のスクリーンショットを次に示します。

![umdf i/o 要求のパフォーマンスのグラフ](images/WpaKMDFIoCapture-Narrow.PNG)

## <a name="pnp-power-callback-graph-and-summary-table"></a>PnP 電源コールバックのグラフと概要テーブル


WPT は、各 PnP と電源コールバックの処理時間を表示することもできます。 次のスクリーンショットは、サンプル KMDF ドライバーとサンプルの UMDF ドライバーの[*EvtDeviceD0Entry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)、 [*EvtDeviceD0Exit*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit) 、および[*evtdevicehardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)のコールバック時間を示しています。

WdfDevice 列には、コールバックに関連付けられている WDFDEVICE ハンドルが含まれています。 ActivityID には、コールバックインスタンスの一意の識別子が含まれています。

![pnp 電源コールバックグラフ](images/wpa-fx2-pnppwr.PNG)

## <a name="which-calls-are-instrumented"></a>どの呼び出しがインストルメント化されますか。


ここでは、上に示したグラフおよびテーブルの作成に使用されるイベントについて説明します。

特定のドライバーに対して WdfPerfEnhancedVerifier を実行した後、システムが指定されたドライバーのコールバックの一部を呼び出したときと、指定されたドライバーがいくつかのフレームワークメソッドを呼び出すと、フレームワークは ETL トレースログにイベントを記録します。

I/o 要求がいつ開始されるかを判断するために、フレームワークは次のコールバックを呼び出すときにイベントを記録します。

-   [*EvtIoDefault*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default)
-   [*EvtIoRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)
-   [*EvtIoWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)
-   [*EvtIoDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)
-   [*EvtIoInternalDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control)

また、このフレームワークは、ドライバーが次のメソッドを呼び出したときに、i/o 要求開始イベントを記録します。

-   [**WdfIoQueueRetrieveNextRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueretrievenextrequest)
-   [**WdfIoQueueRetrieveRequestByFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueretrieverequestbyfileobject)
-   [**WdfIoQueueRetrieveFoundRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueretrievefoundrequest)

I/o 要求が完了したことを確認するために、次のようにドライバーがを呼び出すタイミングがフレームワークによって追跡されます。

-   [**WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)
-   [**WdfRequestCompleteWithInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)
-   [**Wdfrequestcompletewith優先順位ブースト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost)

最後に、PnP/電源コールバックのコールバック時間を決定するために、次のドライバーによって提供されるコールバックルーチンと完了時に、フレームワークによってが記録されます。

-   [*EvtDeviceD0Entry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)
-   [*EvtDeviceD0Exit*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)
-   [*EvtDevicePrepareHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)
-   [*EvtDeviceReleaseHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)
-   [*EvtIoStop*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)

## <a name="resources-and-troubleshooting"></a>リソースとトラブルシューティング


-   WdfPerfEnhancedVerifier スクリプトを実行した後、必ず再起動してください。
-   ドライバーがイベントログを記録するように構成されているかどうかを判断するには、を使用します **。WdfKd. wdfdriverinfo**カーネルデバッガーコマンド。 ドライバーがパフォーマンストレース用に構成されている場合は、次のような出力が表示されます。

    ```cpp
    !WdfKd.WdfDriverInfo Echo.sys
    …
    …
    ----------------------------------

    WDF Verifier settings for echo.sys is ON
      Enhanced verifier: performance analysis hooking ON
    ----------------------------------
    ```

-   開発とテストのみを目的として、ドライバーコード署名ポリシーの適用を一時的に無効にすることができます。 詳細については、「[開発およびテスト中の署名](https://docs.microsoft.com/windows-hardware/drivers/install/installing-an-unsigned-driver-during-development-and-test)されていないドライバーパッケージのインストール」を参照してください。
-   Windows 10 Mobile でトレースをキャプチャした場合は、ターゲットデバイスの MyPerfTrace .etl を、Wpa がインストールされているコンピューターにコピーする必要があります。 これを行うには、 [Tshell ツール](https://sysdev.microsoft.com/Hardware/oem/docs/Phone_Testing/TShell)を使用します。

## <a name="related-topics"></a>関連トピック


[Windows Performance Analyzer](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/hh448170(v=win.10))










