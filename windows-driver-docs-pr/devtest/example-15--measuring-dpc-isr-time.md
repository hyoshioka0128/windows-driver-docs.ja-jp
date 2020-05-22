---
title: 例 15 DPC/ISR 時間の測定
description: 例 15 DPC/ISR 時間の測定
ms.assetid: 47936b8b-fd04-44dc-9cd9-77e9d89b4499
keywords:
- 遅延プロシージャ呼び出しの WDK ソフトウェアトレース
- Dpc WDK ソフトウェアのトレース
- 割り込みサービスルーチン WDK ソフトウェアトレース
- Isr WDK ソフトウェアのトレース
- 時間 WDK ソフトウェアのトレース
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f16f61a0648175bb53390e8b482f9d71da4821a
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769680"
---
# <a name="example-15-measuring-dpcisr-time"></a>例 15: DPC/ISR 時間を測定する


## <span id="ddk_measuring_dpc_isr_time_tools"></span><span id="DDK_MEASURING_DPC_ISR_TIME_TOOLS"></span>


ドライバーが遅延プロシージャ呼び出し (Dpc) と割り込みサービスルーチン (Isr) で費やした時間を測定するには、Windows カーネルでこれらのイベントをトレースします。 この情報は、ドライバーが IRQLs に費やす時間を最小限に抑えるのに役立ちます。これにより、ドライバーとシステムの効率を高めることができます。

Dpc は、100マイクロ秒を超えて実行しないようにすることをお勧めします。また、Isr は25マイクロ秒より長く実行することはできません。 最新の要件については、「[ハードウェアラボキット](https://docs.microsoft.com/windows-hardware/test/hlk/)」を参照してください。

ここでは、次の手順について説明します。

1.  DPC/ISR イベントのカーネルトレースを開始します。

2.  失われたイベントのトレースセッションを監視し、必要に応じてトレースバッファーのサイズを増やします。

3.  テストドライバーを実行します。

4.  トレースセッションを停止します。

5.  Tracerpt を使用して、DPC/ISR アクティビティを要約するレポートを生成します。

6.  レポートの分析

### <a name="span-idstep_1__start_a_trace_session_spanspan-idstep_1__start_a_trace_session_spanstep-1-start-a-trace-session"></a><span id="step_1__start_a_trace_session_"></span><span id="STEP_1__START_A_TRACE_SESSION_"></span>手順 1: トレースセッションを開始します。

次のコマンドは、NT カーネルロガートレースセッションを開始します。

```
tracelog -start -f test01.etl -dpcisr -UsePerfCounter -b 64
```

**トレースログ-start**コマンドを実行すると、トレースセッションが開始されます。 "NT カーネル Logger" は既定のセッション名なので、指定する必要はなく、 **-guid**パラメーターを使用してプロバイダーファイルを指定することはできません。 このコマンドは、 **-f**パラメーターを使用してログセッションを示し、トレースメッセージを*test01*イベントトレースログファイルに送信します。

このコマンドには、Dpc、Isr、コンテキストスイッチ、およびイメージの読み込みのトレースを有効にするための **-dpcisr**パラメーターが含まれています。

Dpc と Isr をトレースする場合は、常に **-useperfcounter**パラメーターをコマンドに追加します。 システムタイマーの解像度が低すぎるため、これらのアクティビティに費やされた時間を計測できません。 また、DPC/ISR イベントをフォーマットするツールである Tracerpt では、レポートのパフォーマンスカウンターのクロック値が必要になります。 (Tracerpt は Windows XP 以降のバージョンの Windows に含まれています)。

最後に、 **-b**パラメーターを使用して、トレースバッファーのサイズを 64 KB に増やします。 DPC/ISR トレースによって大量のトレースメッセージが高速に生成されるため、イベントが失われないようにトレースバッファーのサイズを増やすことが重要です。

このコマンドに応答して、Tracelog は NT カーネルロガーセッションを開始し、そのプロパティを表示します。

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

DPC、ISR、およびコンテキストの切り替えイベントは、表示の [**有効なトレース**] フィールドに表示されないことに注意してください。 これらのイベントは内部インストルメンテーションによって監視されるため、有効になっている場合でも、この一覧には表示されません。 ただし、 **-dpcisr**パラメーターでも有効になっているイメージ読み込みイベントが表示されます。

### <a name="span-idstep_2__check_for_lost_events_spanspan-idstep_2__check_for_lost_events_spanstep-2-check-for-lost-events"></a><span id="step_2__check_for_lost_events_"></span><span id="STEP_2__CHECK_FOR_LOST_EVENTS_"></span>手順 2: 失われたイベントを確認します。

**トレースログ-q** (クエリ) コマンドを定期的に使用して、失われたイベントを確認します。 見つかった場合は、**トレースログ-update**コマンドを使用して、トレースセッションにバッファーを追加します。

```
tracelog -q
```

**トレースログ-q**コマンドはセッション名を受け取りますが、この場合は "NT Kernel Logger" が既定値であるため、指定する必要はありません。

このコマンドに応答して、Tracelog はセッションのプロパティを表示します。

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

この場合、生成された544イベントはバッファーに保存されませんでした。 これが繰り返し発生しないようにするには、**トレースログ-update**コマンドを使用して各バッファーのサイズを増やすか (**-b**)、バッファーの最大数 (**-max**) を増やします。次に例を示します。

```
tracelog -update -b 128 -max 40
```

### <a name="span-idstep_3__exercise_the_driver_spanspan-idstep_3__exercise_the_driver_spanstep-3-exercise-the-driver"></a><span id="step_3__exercise_the_driver_"></span><span id="STEP_3__EXERCISE_THE_DRIVER_"></span>手順 3: ドライバーを実行します。

テストルーチンを使用して、ドライバーがその機能を実行するようにします。 2つのテストを実行することを検討してください。1つは基本機能用で、もう1つは高度な関数用です。

### <a name="span-idstep_4__stop_the_trace_session_spanspan-idstep_4__stop_the_trace_session_spanstep-4-stop-the-trace-session"></a><span id="step_4__stop_the_trace_session_"></span><span id="STEP_4__STOP_THE_TRACE_SESSION_"></span>手順 4: トレースセッションを停止します。

次のコマンドを使用して、トレースセッションを停止します。

```
tracelog -stop
```

通常、**トレースログ stop**コマンドにはセッション名が必要ですが、"NT Kernel Logger" が既定値であるため、セッション名は必要ありません。

### <a name="span-idstep_5__create_a_dpc_isr_report_spanspan-idstep_5__create_a_dpc_isr_report_spanstep-5-create-a-dpcisr-report"></a><span id="step_5__create_a_dpc_isr_report_"></span><span id="STEP_5__CREATE_A_DPC_ISR_REPORT_"></span>手順 5: DPC/ISR レポートを作成する。

イベントトレースログで DPC/ISR メッセージを要約するには、Windows XP SP2 以降のバージョンの Windows に含まれている Tracerpt のバージョンを使用します。

次の Tracerpt コマンドは、 *Test01*ファイル内のメッセージを書式設定し、WINDOWS XP SP2 で、このアクティビティのテキスト形式のレポートを作成します。

```
tracerpt test01.etl -report dpcisr.txt -df
```

このコマンドでは、 **-report**パラメーターを指定して、分析の方法と出力ファイルの名前を指定します。 **-Df**パラメーターは、WINDOWS XP SP2 でのみメッセージを正しく書式設定するために必要です。

Windows Server 2003 SP1 以降のバージョンの Windows でこのレポートを作成する場合は、次のコマンドを使用して HTML 形式のレポートを作成できます。

```
tracerpt test01.etl -report dpcisr.html -f HTML
```

このコマンドでは、 **-report**パラメーターで出力ファイルの名前を指定し、 **-f**パラメーターでレポート形式を指定します。

### <a name="span-idstep_6__analyze_the_report_spanspan-idstep_6__analyze_the_report_spanstep-6-analyze-the-report"></a><span id="step_6__analyze_the_report_"></span><span id="STEP_6__ANALYZE_THE_REPORT_"></span>手順 6: レポートを分析する

"Windows イベントトレースセッションレポート" には、次のセクションがあります。

-   **画像の統計情報。** トレース中にコンピューター上で実行されているプロセスに関するデータを表示します。

-   **ディスクの合計。** トレース中に実行されている各プロセスのディスク i/o に関するデータを表示します。

-   **トレース全体の DPC プロセッサ使用率:** 各ドライバーの DPC ルーチンの処理に費やされたプロセッサ時間の割合を表示します。

-   **トレース全体のすべての DPC 実行時間の分布**。 時間の範囲のテーブル (マイクロ秒単位)。 テーブルには、各時間範囲に含まれる DPC ルーチンの割合が表示されます。

-   **トレース全体に対するドライバーなし (DPCRoutineAddress) DPC 実行時間の分布。** 時間の範囲のテーブル (マイクロ秒単位)。 このテーブルには、この DPC ルーチンのインスタンスのうち、各時間範囲に含まれるインスタンスの割合が表示されます。 このようなセクションは、トレースの DPC ルーチンごとに表示されます。

-   **トレース全体の ISR プロセッサ使用率。** トレース内の各ドライバーの割り込みサービスルーチンの処理に費やされたプロセッサ時間の割合を表示します。

-   **トレース全体のすべての ISR 実行時間の分布。** 時間の範囲のテーブル (マイクロ秒単位)。 テーブルには、各時間範囲に含まれる ISR ルーチンの割合が表示されます。

-   **トレース全体に対して、ドライバー (ISRAddress) ISR の実行時間の分布。** 時間の範囲のテーブル (マイクロ秒単位)。 このテーブルには、各時間範囲に含まれる ISR のインスタンスの割合が表示されます。 このようなセクションは、トレース内のすべての ISR で表示されます。

-   **TracingPeriodInMs 2 マイクロ秒の時間帯の DPC と ISR のプロセッサ使用率の分布。** トレース中に、Dpc と Isr によるプロセッサ使用率の合計を表示します。

-   **トレース全体に対して、ドライバーの (ISRAddress) ISR からドライバー間 (DPCRoutineAddress) DPC 待機時間の分布。** ISR の終わりと関連する DPC の先頭との間の遅延間隔の分布を表示します。

次のサンプルレポートの抜粋は、Ipsec の DPC の実行時間の分布を示しています。 一般に、DPC ルーチンは100マイクロ秒以上の持続を推奨しています。 このレポートには、このドライバーの半分を超える DPC ルーチンがしきい値を超えていることが示されています。

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

 

 





