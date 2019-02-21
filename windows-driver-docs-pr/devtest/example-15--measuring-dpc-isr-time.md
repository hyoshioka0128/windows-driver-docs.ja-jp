---
title: 15 の例を測定する DPC ISR/時間
description: 15 の例を測定する DPC ISR/時間
ms.assetid: 47936b8b-fd04-44dc-9cd9-77e9d89b4499
keywords:
- 遅延プロシージャ呼び出しの WDK ソフトウェア トレース
- Dpc WDK ソフトウェア トレース
- 割り込みサービス ルーチン WDK ソフトウェア トレース
- Isr WDK ソフトウェア トレース
- 時間の WDK ソフトウェア トレース
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c9469b55a507c14727e566bf610541f4e960308
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560598"
---
# <a name="example-15-measuring-dpcisr-time"></a>15 の使用例:DPC/ISR 時間を測定します。


## <span id="ddk_measuring_dpc_isr_time_tools"></span><span id="DDK_MEASURING_DPC_ISR_TIME_TOOLS"></span>


ドライバーが遅延プロシージャ呼び出し (Dpc) に費やされた時間を測定し、Windows カーネルでこれらのイベントをトレースすることで割り込みサービス ルーチン (Isr) できます。 この情報は、ドライバーがドライバーとシステムをより効率的に行うより高い Irql で費やす時間を最小限にできます。

Dpc を 100 マイクロ秒より長く実行しないでください、Isr を 25 (マイクロ秒) よりも長く実行しないでくださいことを Microsoft がお勧めします。 最新の要件を参照して、[ハードウェア認定プログラム]( https://go.microsoft.com/fwlink/p/?linkid=227016)します。

このセクションで説明されている手順には、次の手順が含まれています。

1.  DPC/ISR イベントのカーネル トレースを開始します。

2.  削除されるイベントのトレース セッションを監視し、必要に応じて、トレース バッファーのサイズを大ききます。

3.  ドライバーのテストを実行します。

4.  トレース セッションを停止します。

5.  Tracerpt を使用すると、DPC/ISR アクティビティを要約したレポートを生成します。

6.  レポートを分析します。

### <a name="span-idstep1startatracesessionspanspan-idstep1startatracesessionspanstep-1-start-a-trace-session"></a><span id="step_1__start_a_trace_session_"></span><span id="STEP_1__START_A_TRACE_SESSION_"></span>手順 1:トレース セッションを開始します。

次のコマンドは、NT Kernel Logger トレース セッションを開始します。

```
tracelog -start -f test01.etl -dpcisr -UsePerfCounter -b 64
```

**Tracelog-開始**コマンド トレース セッションを開始します。 "NT Kernel Logger"は、既定のセッションの名前、それを指定する必要はありません、および使用することはできませんので、 **- guid**プロバイダー ファイルを指定するパラメーター。 コマンドを使用して、 **-f**にメッセージをトレースに出力するためのパラメーターをログ セッションを示すために、 *test01.etl*イベント トレース ログ ファイル。

コマンドが含まれています、 **- dpcisr**パラメーター Dpc、isr を特定、コンテキストの切り替え、およびイメージの読み込みのトレースを有効にします。

Dpc と isr を特定のトレース、ときにいつでも追加、 **- UsePerfCounter**パラメーターをコマンド。 システムのタイマー精度が小さすぎる場合、これらのアクティビティに費やされた時間を測定します。 また、Tracerpt、DPC/ISR イベントでは、書式設定ツールでは、そのレポートのパフォーマンス カウンターのクロック値が必要です。 (Tracerpt は、Windows XP および Windows の以降のバージョンに含まれています)。

最後に、コマンドを使用して、 **-b**パラメーターを 64 KB にトレース バッファーのサイズを増やします。 DPC/ISR トレースは、大量の急速にトレース メッセージを生成するためには、イベントが失われないように、トレース バッファーのサイズを増やす必要があります。

このコマンドに応答して、トレース ログは NT Kernel Logger セッションを開始し、そのプロパティが表示されます。

```
Logger Started...
Operation Status:       0L      The operation completed successfully.

Logger Name:            NT Kernel Logger
Logger Id:              ffff
Logger Thread Id:       00000C18
Buffer Size:            64 Kb
Maximum Buffers:        25
Minimum Buffers:        3
Number of Buffers:      5
Free Buffers:           4
Buffers Written:        14
Events Lost:            0
Log Buffers Lost:       0
Real Time Buffers Lost: 0
AgeLimit:               15
Log File Mode:          Sequential
Enabled tracing:        Process Thread Disk File ImageLoad
Log Filename:           c:\Tracelog\test01.etl
```

DPC、ISR、およびコンテキストの切り替えイベントに表示されないことに注意してください、**有効トレース**表示のフィールド。 これらのイベントが内部のインストルメンテーションによって監視が表示されないこの一覧にもためそれらが有効な場合。 ただし、イメージの読み込みイベントで有効になっても、 **- dpcisr**パラメーターを表示しないでください。

### <a name="span-idstep2checkforlosteventsspanspan-idstep2checkforlosteventsspanstep-2-check-for-lost-events"></a><span id="step_2__check_for_lost_events_"></span><span id="STEP_2__CHECK_FOR_LOST_EVENTS_"></span>手順 2:失われたイベントを確認します。

使用して、 **tracelog q**失われたイベントを確認するには、定期的に (クエリ) コマンド。 その場合を使用して、 **tracelog-更新**トレース セッションに複数のバッファーを追加するコマンド。

```
tracelog -q
```

**Tracelog q**コマンドは、セッション名を受け取りますが、"NT Kernel Logger"が既定値であるためここで提供する必要はありません。

このコマンドに応答して、トレース ログには、セッションのプロパティが表示されます。

```
Operation Status:       0L      The operation completed successfully.

Logger Name:            NT Kernel Logger
Logger Id:              ffff
Logger Thread Id:       00000BC4
Buffer Size:            64 Kb
Maximum Buffers:        25
Minimum Buffers:        3
Number of Buffers:      25
Free Buffers:           23
Buffers Written:        571
Events Lost:            544
Log Buffers Lost:       0
Real Time Buffers Lost: 0
AgeLimit:               15
Log File Mode:          Sequential
Enabled tracing:        Process Thread Disk File ImageLoad
Log Filename:           c:\Tracelog\test.etl
```

この場合、生成されたイベントが 544 はバッファーに保存されませんでした。 定期的なからこれを回避するには使用、 **tracelog-更新**コマンドを各バッファーのサイズを増やす (**-b**) またはバッファーの最大数を増やす (**-最大**) の例:

```
tracelog -update -b 128 -max 40
```

### <a name="span-idstep3exercisethedriverspanspan-idstep3exercisethedriverspanstep-3-exercise-the-driver"></a><span id="step_3__exercise_the_driver_"></span><span id="STEP_3__EXERCISE_THE_DRIVER_"></span>手順 3:ドライバーを実行します。

ドライバーの機能を実行するのにテスト ルーチンを使用します。 基本的な機能と高度な関数の 2 つのテストを実行することを検討してください。

### <a name="span-idstep4stopthetracesessionspanspan-idstep4stopthetracesessionspanstep-4-stop-the-trace-session"></a><span id="step_4__stop_the_trace_session_"></span><span id="STEP_4__STOP_THE_TRACE_SESSION_"></span>手順 4:トレース セッションを停止します。

トレース セッションを停止するのにには、次のコマンドを使用します。

```
tracelog -stop
```

A **tracelog-停止**コマンドには、セッション名では、通常必要がありますが、"NT Kernel Logger"は、既定値であるため、セッション名は必要ありません。

### <a name="span-idstep5createadpcisrreportspanspan-idstep5createadpcisrreportspanstep-5-create-a-dpcisr-report"></a><span id="step_5__create_a_dpc_isr_report_"></span><span id="STEP_5__CREATE_A_DPC_ISR_REPORT_"></span>手順 5:DPC/ISR レポートを作成します。

イベント トレース ログには、DPC/ISR メッセージをまとめると、Windows XP SP2、および以降のバージョンの Windows に含まれる Tracerpt のバージョンを使用します。

次の Tracerpt コマンド内のメッセージを書式設定、 *Test01.etl*ファイルし、Windows XP SP2 でのアクティビティのテキスト形式のレポートを作成します。

```
tracerpt test01.etl -report dpcisr.txt -df
```

このコマンドで、 **-レポート**パラメーターは、分析の方法と、出力ファイルの名前を指定します。 **-Df** Windows XP SP2 でのみ、メッセージを正しく書式設定するパラメーターが必要です。

Windows Server 2003 SP1 と以降のバージョンの Windows でこのレポートを作成するときに、次のコマンドを使用して、HTML 形式のレポートを作成できます。

```
tracerpt test01.etl -report dpcisr.html -f HTML
```

このコマンドで、 **-レポート**パラメーター、出力ファイルの名前を指定し、 **-f**パラメーターをレポート形式を指定します。

### <a name="span-idstep6analyzethereportspanspan-idstep6analyzethereportspanstep-6-analyze-the-report"></a><span id="step_6__analyze_the_report_"></span><span id="STEP_6__ANALYZE_THE_REPORT_"></span>手順 6:レポートを分析します。

「Windows イベント トレース セッション レポート」には、次のセクションがあります。

-   **イメージの統計情報です。** トレース中に、コンピューターで実行されているプロセスに関するデータを表示します。

-   **ディスクの合計。** ディスク I/O、トレース中に実行されている各プロセスに関するデータを表示します。

-   **全体のトレースのプロセッサ使用率の DPC:** プロセッサ時間サービス DPC ルーチンの各ドライバーの割合を表示します。

-   **全体のトレースの DPC 実行時間がすべての配布**します。 マイクロ秒単位の時間範囲のテーブル。 テーブルには、各時間の範囲に分類される DPC ルーチンの割合が表示されます。

-   **ドライバー名 (DPCRoutineAddress) DPC の分布全体のトレースの実行時間。** マイクロ秒単位の時間範囲のテーブル。 テーブルには、各時間の範囲に分類されるこの DPC ルーチンのインスタンスの割合が表示されます。 このいずれかのようなセクションでは、トレースにすべて DPC ルーチンが表示されます。

-   **全体のトレースの ISR プロセッサ使用率。** サービスに費やしたプロセッサ時間の割合が表示されます、割り込みサービス ルーチン、トレースでは、各ドライバー。

-   **全体のトレースの ISR 実行時間がすべての配布。** マイクロ秒単位の時間範囲のテーブル。 テーブルには、各時間の範囲に分類される ISR ルーチンの割合が表示されます。

-   **ドライバー名 (ISRAddress) ISR の分布全体のトレースの実行時間。** マイクロ秒単位の時間範囲のテーブル。 テーブルには、各時間の範囲に分類される ISR のインスタンスの割合が表示されます。 すべての ISR トレースにこのいずれかのようなセクションが表示されます。

-   **2 つのマイクロ秒単位の時間ウィンドウ TracingPeriodInMs DPC と ISR のプロセッサ使用率の分布。** Dpc isr を特定して、トレース中に結合されたプロセッサ使用率を表示します。

-   **ドライバー名 (ISRAddress) ISR DriverName (DPCRoutineAddress) DPC の配布、全体のトレースの待機時間。** ISR の末尾と関連付けられている DPC の先頭の間の遅延間隔の分布が表示されます。

次のサンプル レポートからの抜粋では、ある Ipsec.sys の DPC 実行時間の分布を示します。 一般に、DPC ルーチンの継続期間が 100 を超える (マイクロ秒) は推奨されません。 レポートでは、ドライバーの DPC ルーチンの半分以上のしきい値を超えていることを示します。

```
+------------------------------------------------------------------------------+
| Distribution of ipsec.sys (F7AA7449) DPC execution times for the whole trace |
+------------------------------------------------------------------------------+
| Lower Bound         Upper Bound            Count             Percent         |
+------------------------------------------------------------------------------+
|           0                   1                0                0.00%        |
|           1                   2                0                0.00%        |
|           2                   3                8               42.11%        |
|           3                   4                1                5.26%        |
|           4                   5                0                0.00%        |
|           5                  10                0                0.00%        |
|          10                  25                0                0.00%        |
|          25                  50                0                0.00%        |
|          50                 100                0                0.00%        |
|         100                 250               10               52.63%        |
+------------------------------------------------------------------------------+
|                                               19              100.00%        |
+------------------------------------------------------------------------------+
```

 

 





