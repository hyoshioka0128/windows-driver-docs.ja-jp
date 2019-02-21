---
title: TraceLogging データのキャプチャと表示
description: TraceLogging データのキャプチャと表示
ms.assetid: E5C18352-B05B-42BF-B5B8-12ABA0E6131C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b2ae5606fdff07fc29b8d8bd8ac0d1a80f60232
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536049"
---
# <a name="capture-and-view-tracelogging-data"></a>TraceLogging データのキャプチャと表示


キャプチャして TraceLoggging を最新の内部バージョンの Windows パフォーマンス ツール (WPT) を使用してデータを表示することができます。 インストルメンテーションを公開する前に、イベント データが生成され、適切なタイミングで意味のあるデータが生成されることを確認する TraceLogging プロバイダー コードをテストする必要があります。

確認するプロセスには、インストルメンテーションが正しいこと、2 つの手順が含まれます。

-   Windows Performance Recorder (wpr.exe または wprui.exe) では、トレースをキャプチャします。
-   Windows パフォーマンス アナライザー (wpa.exe) を使用してトレースを表示します。

**注**、Windows Phone を使用することできますも Tracelog.exe と Xperf.exe トレースをキャプチャします。 (トレース、XPerf を使用して) 電話でのトレースをキャプチャするには"するには」を参照してください。



### <a name="span-idprerequisitesspanspan-idprerequisitesspanspan-idprerequisitesspanprerequisites"></a><span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>前提条件

WPR および WPA ツール TraceLogging に対してリンクされているのバージョンと互換性があります。 キャプチャ、または、イベントをデコードできない場合は、可能性があります、ツールが一致しないとは互換性がありません。

### <a name="span-idtocapturetracedatawithwprspanspan-idtocapturetracedatawithwprspanspan-idtocapturetracedatawithwprspanto-capture-trace-data-with-wpr"></a><span id="To_capture_trace_data_with_WPR"></span><span id="to_capture_trace_data_with_wpr"></span><span id="TO_CAPTURE_TRACE_DATA_WITH_WPR"></span>WPR でトレース データをキャプチャするには

1.  作成または、TraceLoggingProvider の WPR プロファイル (.wprp) を編集します。

    次の例を使用することができます。 .Wprp ファイル名拡張子を持つファイルに内容を保存します。 TODO セクションをプロバイダーの適切な値に置き換えます。 たとえば、GUID によってプロバイダーを登録する場合は、このファイルの GUID を指定します。

    **注**カーネル モード プロバイダーは、追加 NonPagedMemory ="true"EventProvider の Id 要素では、次の XML の例では、コメントを参照してください。




サンプル WPRP ファイル:

```
<?xml version="1.0" encoding="utf-8"?>
<!-- TODO: 
1. Find and replace "WorkshopTraceLoggingProvider" with your component name.
2. See TODO below to update GUID for your event provider
-->
<WindowsPerformanceRecorder Version="1.0" Author="Microsoft Corporation" 
    Copyright="Microsoft Corporation" Company="Microsoft Corporation">
  <Profiles>
    <EventCollector Id="EventCollector_WorkshopTraceLoggingProvider" 
      Name="WorkshopTraceLoggingProviderCollector">
      <BufferSize Value="64" />
      <Buffers Value="4" />
    </EventCollector>

<!-- TODO: 
 1. Update Name attribute in EventProvider xml element with your provider GUID, 
    or if you specify an EventSource C# provider or call TraceLoggingRegister(...) 
    without a GUID, use star(*) before your provider name, 
    eg: Name="*MyEventSourceProvider" which will enable your provider appropriately.
 2. This sample lists more than 1 EventProvider xml element and references them again 
    in a Profile with EventProviderId xml element. For your component wprp, enable 
    the required number of providers and fix the Profile xml element appropriately
--> 
    <EventProvider Id="EventProvider_WorkshopTraceLoggingProvider" 
      Name="f9bc6c5d-4b98-43b5-90a1-1d0c8f45bf5a" />
<!-- For Kernel Mode providers, add NonPagedMemory="true" attribute to the 
  EventProvider Id element:

  Example:
  <EventProvider Id="EventProvider_UMDFReflector" 
    Name="263dd596-513b-4fd9-969c-022b691bb130" NonPagedMemory="true"/> 

-->

    <Profile Id="WorkshopTraceLoggingProvider.Verbose.File" 
      Name="WorkshopTraceLoggingProvider" Description="WorkshopTraceLoggingProvider" 
      LoggingMode="File" DetailLevel="Verbose">
      <Collectors>
        <EventCollectorId Value="EventCollector_WorkshopTraceLoggingProvider">
          <EventProviders>
<!-- TODO:
 1. Fix your EventProviderId with Value same as the Id attribute on EventProvider 
    xml element above
-->
            <EventProviderId Value="EventProvider_WorkshopTraceLoggingProvider" />
          </EventProviders>
        </EventCollectorId>
      </Collectors>
    </Profile>

    <Profile Id="WorkshopTraceLoggingProvider.Light.File" 
      Name="WorkshopTraceLoggingProvider" 
      Description="WorkshopTraceLoggingProvider" 
      Base="WorkshopTraceLoggingProvider.Verbose.File" 
      LoggingMode="File" 
      DetailLevel="Light" />

    <Profile Id="WorkshopTraceLoggingProvider.Verbose.Memory" 
      Name="WorkshopTraceLoggingProvider" 
      Description="WorkshopTraceLoggingProvider" 
      Base="WorkshopTraceLoggingProvider.Verbose.File" 
      LoggingMode="Memory" 
      DetailLevel="Verbose" />

    <Profile Id="WorkshopTraceLoggingProvider.Light.Memory" 
      Name="WorkshopTraceLoggingProvider" 
      Description="WorkshopTraceLoggingProvider" 
      Base="WorkshopTraceLoggingProvider.Verbose.File" 
      LoggingMode="Memory" 
      DetailLevel="Light" />

  </Profiles>
</WindowsPerformanceRecorder>
```


2.  カーネル モード プロバイダーの場合、NonPagedMemory を追加する必要があります。 EventProvider の Id 要素に属性を"true"を = です。

    ```
    <EventProvider Id="EventProvider_myTraceLoggingProviderKM" 
      Name="263dd596-513b-4fd9-969c-022b691bb130" NonPagedMemory="true"/>
    ```

3.  ファイル名拡張子を持つファイルを保存 (します。WPRP)。
4.  コマンド プロンプト ウィンドウから WPR を使用してキャプチャを開始します。

    ```
    <path to wpr>\wpr.exe -start GeneralProfile -start  yourTraceLoggingProvider.wprp
    ```

    GeneralProfile、システム イベントがキャプチャされます。 一般的なデバッグでは、プロバイダーからイベントと共に、システム イベントをキャプチャすることをお勧めを勧めします。

5.  テスト シナリオを実行 (ロードおよびアンロード、ドライバーまたはイベントを発生させるコンポーネント)。
6.  トレースのキャプチャを停止し、すべての記録をマージします。

    ```
    <path to wpr>\wpr.exe -stop GeneralProfile -stop  yourTraceCaptureFile.etl description
    ```

トレース データを収集するのにパフォーマンス レコーダーの Windows ユーザー インターフェイス (Wprui.exe) を使用することもできます。

```
<path to wpr>\wprui.exe
```

1.  WPR ウィンドウで、オプションが非表示の場合 をクリックして**オプションより**します。
2.  クリックして**プロファイルの追加**.wprp ファイルの場所に移動します。
3.  .Wprp ファイルを選択し、クリックして**オープン**します。 WPR では、プロファイルの XML スキーマを検証します。
4.  クリックして**開始**し、テスト シナリオを実行します。
5.  クリックして**保存**結果をマージし、ファイルに保存します。 WPR ユーザー インターフェイスを使用する場合は、WPA で .etl のログ ファイルを開くためのオプションも付与されます。

### <a name="span-idtocapturetraceonphoneusingtracelogandxperfspanspan-idtocapturetraceonphoneusingtracelogandxperfspanspan-idtocapturetraceonphoneusingtracelogandxperfspanto-capture-trace-on-phone-using-tracelog-and-xperf"></a><span id="To_capture_trace_on_Phone__using_Tracelog_and_XPerf_"></span><span id="to_capture_trace_on_phone__using_tracelog_and_xperf_"></span><span id="TO_CAPTURE_TRACE_ON_PHONE__USING_TRACELOG_AND_XPERF_"></span>(トレース、XPerf を使用して) 電話でのトレースをキャプチャするには

1.  プロバイダーのトレース キャプチャを開始します。

    ```
    cmdd tracelog '-start test -f c:\test.etl -guid #providerguid'
    ```

2.  イベントをログに、テスト シナリオを実行します。
3.  トレースのキャプチャを停止します。

    ```
    cmdd tracelog '-stop test'
    ```

4.  トレース結果をマージします。

    ```
    cmdd xperf -merge c:\test.etl c:\testmerged.etl
    ```

5.  マージされたログ ファイルを取得します。

    ```
    getd c:\testmerged.etl
    ```

### <a name="span-idviewtraceloggingdatausingwpaspanspan-idviewtraceloggingdatausingwpaspanspan-idviewtraceloggingdatausingwpaspanview-tracelogging-data-using-wpa"></a><span id="View_TraceLogging_data_using_WPA"></span><span id="view_tracelogging_data_using_wpa"></span><span id="VIEW_TRACELOGGING_DATA_USING_WPA"></span>WPA を使用して TraceLogging データの表示

現時点では、WPA は、TraceLogging を生成する etl ファイルを表示する使用できる唯一のビューアーです。

1.  WPA を開始します。

    ```
    <path to wpr>\wpa.exe
    ```

2.  トレース ファイル (.etl) を読み込みます。
3.  プロバイダーのイベントを表示します。 Graph エクスプ ローラーで、**システム アクティビティ**します。
4.  ダブルクリック**汎用イベント**分析ビューを表示します。
5.  分析ビューでログ記録が動作していることを確認するには、プロバイダーからイベントを探します。

    **プロバイダー名**汎用イベント テーブルの列を検索して、プロバイダー名を含む行を選択します。

    列名は、ご利用のプロバイダーを見つけやすい可能性がありますように並べ替える列見出しをクリックすることができます。 ときに、プロバイダー、右クリックし、名前を見つける**フィルター選択を**します。









