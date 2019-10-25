---
title: WDTF トレースの有効化と表示
description: WDTF トレースの有効化と表示
ms.assetid: 9bed6042-3691-4a5e-a143-51acf746b1ae
keywords:
- Windows デバイステストフレームワーク WDK、トレースイベント
- WDTF WDK、トレースイベント
- WDK WDTF のトレース
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6665c1d431c660f5dfa152e013ca30e5a48fddbd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844797"
---
# <a name="enabling-and-viewing-wdtf-traces"></a>WDTF トレースの有効化と表示

WDTF *Tracing*は、wdtf オブジェクト内で内部的に発生するレポートイベントを示します。 WDTF は頻繁にインストルメント化されるため、すべての WDTF オブジェクトは実行時にトレース情報を提供します。 WDTF は、 [WPP ソフトウェアトレース](https://docs.microsoft.com/windows-hardware/drivers/devtest/wpp-software-tracing)を使用してトレースを処理します。 この種類のトレースは、 [Traceview](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-traceview)を含む WDK ツールを使用して読み取ることができる標準化された形式です。 このトピックでは、 [Logman](https://go.microsoft.com/fwlink/p/?linkid=136332)と[tracefmt](https://docs.microsoft.com/windows-hardware/drivers/devtest/tracefmt)を使用して wdtf ランタイムトレースを表示する方法について説明します。 このトピックでは、WDTF トレースレベルをプログラムで構成する方法についても説明します。

## <a name="how-to-collect-and-save-wdtf-traces"></a>WDTF トレースを収集して保存する方法

### <a name="to-start-collecting-wdtf-traces"></a>WDTF トレースの収集を開始するには

1. テストコンピューターで、管理者特権 ( **[管理者として実行]** ) を使用してコマンドプロンプトウィンドウを開き、次のコマンドを入力します。

    ```syntax
    logman.exe create trace "autosession\WDTF" -p {6210f559-c7f7-4d2f-b674-4bc9315cecc7} 0xffffffff 0xff -o c:\WDTF_Traces\TraceFile.etl
    reg add HKLM\SYSTEM\CurrentControlSet\Control\WMI\Autologger\WDTF /v LogFileMode /t REG_DWORD /d 1 /f
    reg add HKLM\SYSTEM\CurrentControlSet\Control\WMI\Autologger\WDTF /v FileMax /t REG_DWORD /d 16 /f
    reg add HKLM\SYSTEM\CurrentControlSet\Control\WMI\Autologger\WDTF /v MaxFileSize /t REG_DWORD /d 0 /f
    ```

2. コンピューターを再起動します。

その他のオプションの詳細については、「 [logman](https://go.microsoft.com/fwlink/p/?linkid=136332) (logman)」を参照してください。 トレース季節の作成の詳細については、「自動[ロガーセッションの構成と開始](https://docs.microsoft.com/windows/desktop/ETW/configuring-and-starting-an-autologger-session)」を参照してください。

### <a name="to-stop-collecting-wdtf-traces-and-save-log-files"></a>WDTF トレースの収集を停止し、ログファイルを保存するには

1. 次のコマンドを使用して、WDTF トレースの収集を停止し、データコレクターを削除できます。

    ```syntax
    logman.exe -stop -ets WDTF
    logman.exe delete "autosession\WDTF"
    ```

2. コンピューターを再起動します。
3. 後で分析するために、テストコンピューターから別のコンピューターにログファイルをコピーします。

    収集される ETL ログファイルのサイズは非常に大きくなることがあります。 最適な結果を得るには、テストコンピューターからログファイルをコピーします (たとえば、c:\\WDTF\_トレース\\トレース) を別のコンピューターにコピーします。 その後、テストコンピューターからログファイルを削除できます。

## <a name="how-to-view-wdtf-traces"></a>WDTF トレースを表示する方法

WDTF トレースを表示するには、ETL ファイルをフォーマットする必要があります。 次の手順では、 [Tracefmt](https://docs.microsoft.com/windows-hardware/drivers/devtest/tracefmt)を使用して、ETL ファイルをテキストファイルまたは CSV ファイルに変換する方法を示します。

### <a name="to-view-wdtf-traces"></a>WDTF トレースを表示するには

1. たとえば、次のコマンドは、c:\\WDTF\_トレース\\TraceFile .etl として保存された ETL ファイルをテキストに変換します。

    ```syntax
    Tracefmt.exe –r http://msdl.microsoft.com/download/symbols c:\WDTF_Traces\TraceFile.etl -o OutputTxtFile.txt
    ```

2. 次のコマンドでは、c:\\WDTF\_トレース\\トレースによって保存された ETL ファイルをコンマ区切りファイル (CSV) に変換します。

    ```syntax
    Tracefmt.exe –r http://msdl.microsoft.com/download/symbols c:\WDTF_Traces\TraceFile.etl -csv –o OutputCsvFile.csv
    ```

3. Excel のフィルター機能を使用して収集されたトレースをフィルター処理できるように、Microsoft Excel で CSV ファイルを開きます。 トレースは、特定の期間に対してフィルター処理できます。 トレースをフィルター処理して、特定の WDTF コンポーネントによって記録されたトレースを調べることができます。

## <a name="programmatically-configuring-wdtf-trace-levels"></a>WDTF トレースレベルのプログラムによる構成

すべての WDTF オブジェクトは、実行時にトレース情報を提供します。

WDTF には、構成可能な一連の[**TTraceLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)レベルが用意されています。 実行時に特定のオブジェクトインスタンスの**TTraceLevel**を設定する方法については、 [**Itracing:: SetTraceLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)メソッドを参照してください。

インターフェイスの既定の[**TTraceLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)を設定する方法の詳細については、「 [Windows デバイステストフレームワークのリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。

各[**TTraceLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)に含まれるトレースの種類の詳細については、 [**ITracer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)インターフェイスの説明を参照してください。 これらのレベルは、 **ITracer**のレジストリ TraceLevel パスを使用して、自分でグローバルに構成することができます。

次の表では、設定できるトレースレベルについて説明します。

|レベル|説明|
|----|----|
|0|[オフ] になっていることを確認します。 トレースが提供されていません。|
|1|低|
|2|程度. このレベルは、トレースの既定のレベルです。|
|3|[高]|
|ホーム フォルダーが置かれているコンピューターにアクセスできない|全角. すべてのトレース情報が報告されます。|
|5-8|カスタムレベル。|
|9|オブジェクトを初期トレースレベルに戻します。|

トレースコンテンツを使用してデバッグする場合は、すべてのオブジェクトについてトレースレベルを1に設定し、調査しているオブジェクトに対してトレースレベルを設定することを検討してください。

トレースレベルの詳細については、「 [**ITracer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)インターフェイス」を参照してください。

## <a name="related-topics"></a>関連トピック

[自動ロガーセッションの構成と開始](https://docs.microsoft.com/windows/desktop/ETW/configuring-and-starting-an-autologger-session)  
[Logman](https://go.microsoft.com/fwlink/p/?linkid=136332)  
[Tracefmt](https://docs.microsoft.com/windows-hardware/drivers/devtest/tracefmt)  
[TraceView](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-traceview)  
[WPP ソフトウェア トレース](https://docs.microsoft.com/windows-hardware/drivers/devtest/wpp-software-tracing)  
