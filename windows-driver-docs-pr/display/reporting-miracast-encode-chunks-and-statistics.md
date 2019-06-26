---
title: Miracast エンコードのチャンクおよび統計情報のレポート
description: ディスプレイ ハードウェアでは、フレームを複数の部分に分割して Miracast ワイヤレス ディスプレイ リンク経由で送信される各ビデオのフレームを処理したり、チャンクをエンコードすることができます。
ms.assetid: E1CE637F-42ED-4BEB-A2FF-04B4B88469DC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7ae24a328531305cb78d9a6916dc59c0bf0e29e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380164"
---
# <a name="reporting-miracast-encode-chunks-and-statistics"></a>Miracast エンコードのチャンクおよび統計情報のレポート


ディスプレイ ハードウェアが、フレームを複数の部分に分割して Miracast ワイヤレス ディスプレイ リンク経由で送信される各ビデオのフレームを処理または*チャンク エンコード*します。 各チャンクは、フレーム数とフレームの一部 (またはスライス) の数から生成される一意のチャンク ID を持ちます。 同じデスクトップのフレームの更新に関連した各チャンクには、同じフレーム番号を割り当てる必要があります。

## <a name="span-idreportingchunkprocessingspanspan-idreportingchunkprocessingspanspan-idreportingchunkprocessingspanreporting-chunk-processing"></a><span id="Reporting_chunk_processing"></span><span id="reporting_chunk_processing"></span><span id="REPORTING_CHUNK_PROCESSING"></span>レポートのチャンクの処理


ドライバーは、Miracast ワイヤレス リンク経由での複数の送信のフレームをエンコードする処理手順-エンコーディングから、色変換を分離する例: または 1 つの手順で。 各処理手順には、フレーム内で一意のフレームの部品番号を割り当てる必要があります。

Miracast ユーザー モード ドライバーまたはディスプレイのミニポート ドライバーのいずれかする必要がありますオペレーティング システムに通知するたびに、ハードウェアのフレームとフレームの各部分がネットワークに送信する直前に、処理手順が完了したことです。 報告された特定の処理手順の時間は、できるだけ迅速に、段階を報告することが重要であるために、オペレーティング システムにイベントが報告された時刻と見なされます。

オペレーティング システムを受け取らないアクション以外の Event Tracing for Windows (ETW) のカーネル レベルのトレース機能を使用してこれらのイベントを記録します。 それでも、こうした情報は、測定して、パフォーマンスの問題の調査にとって重要です。

これらは、方法、ドライバーが、通知を提供できます。

-   Miracast ユーザー モード ドライバーの呼び出し、 [ **ReportStatistic** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_report_statistic)で詳細を報告するコールバック関数、 **MIRACAST\_統計\_型\_チャンク\_処理\_完了**型、または**MIRACAST\_統計\_型\_チャンク\_SENT**に転送用ネットワーク スタックに送信するだけのチャンクが示します。
-   ディスプレイのミニポート ドライバーが、チャンクの処理の詳細を報告、 **DXGK\_割り込み\_MICACAST\_チャンク\_処理\_完了**割り込み入力すると、このレポートは、割り込み時にのみ作成でき、チャンクの情報をログに加え、チャンクのパケットが作成され、Miracast ユーザー モード ドライバーを使用すると呼び出すことによって取得できるようにキューに置かれた、 [ **GetNextChunkData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_get_next_chunk_data)コールバック関数。
-   表示のミニポート ドライバー呼び出し、 [ **DxgkCbReportChunkInfo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkcb_miracast_report_chunk_info) IRQL レベルでのコールバック関数。 この関数は、チャンクの情報のみを記録し、チャンクの任意のパケットをキューに登録しません。

デスクトップのイメージが更新されない、ドライバーは、品質を向上させるためにもう一度デスクトップ イメージのエンコードが必要な場合は、同じフレーム番号や部品番号を使用してください。 パフォーマンス ツールには、2 つ目はトリガーのフレームは同じで、部品番号、同じフレームの 2 つ目のエンコードが実行されたことを示す完全なイベントをエンコードします。

**注**  各フレームの最後のスライスが 0 のフレームの部品番号をいる必要があります。 フレームのスライスの最後であるパフォーマンス ツールを示すこれを行います。

 

正しいことを確認するのには、エンコーディングが、要求されたピクセル パイプラインによって実行される場合、プライマリのサーフェイス上の同期は、エンコードが完了、プライマリの画面にアクセスする前に、間隔を報告する必要がない VSync で操作を反転します。 これにより、プレゼンター レンダリングをプライマリの画面にエンコード エンジンがそこから読み取り中になります。

Miracast ユーザー モード ドライバーは、各フレームの処理のいくつかの段階でオペレーティング システムに通知する必要があります。

<span id="Start_frame__chunk_type__MIRACAST_CHUNK_TYPE_FRAME_START_"></span><span id="start_frame__chunk_type__miracast_chunk_type_frame_start_"></span><span id="START_FRAME__CHUNK_TYPE__MIRACAST_CHUNK_TYPE_FRAME_START_"></span>フレームを起動し、チャンクの種類を**MIRACAST\_チャンク\_型\_フレーム\_開始**:  
オペレーティング システムが新しいデスクトップ フレームを表示するドライバーを確認するポイントを表します。 技術的にはこれを報告する Miracast ユーザー モード ドライバーから、新しいフレームの処理の開始は常にディスプレイのミニポート ドライバーでは、ドライバーによって報告する必要があります。

<span id="Color_convert_complete__chunk_type_MIRACAST_CHUNK_TYPE_COLOR_CONVERT_COMPLETE_"></span><span id="color_convert_complete__chunk_type_miracast_chunk_type_color_convert_complete_"></span><span id="COLOR_CONVERT_COMPLETE__CHUNK_TYPE_MIRACAST_CHUNK_TYPE_COLOR_CONVERT_COMPLETE_"></span>変換の完全な色、チャンクの種類を**MIRACAST\_チャンク\_型\_色\_変換\_完了**:  
一部のソリューションでは、別の色に変換し、エンコード ステージがあります。 このようなソリューションで、色変換処理の完了イベントをできるだけ早く報告するかし、ドライバーを使用する必要があります、 [ **DXGK\_MIRACAST\_チャンク\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-dxgk_miracast_chunk_info).**ProcessingTime**ハードウェアの操作を実行するにかかった時間を報告するメンバー。 フレーム全体がスライスではなく、一度にすべてを変換する色である場合は、部品番号は 0 にする必要があります。

<span id="Encode_complete__chunk_type_MIRACAST_CHUNK_TYPE_ENCODE_COMPLETE_"></span><span id="encode_complete__chunk_type_miracast_chunk_type_encode_complete_"></span><span id="ENCODE_COMPLETE__CHUNK_TYPE_MIRACAST_CHUNK_TYPE_ENCODE_COMPLETE_"></span>完全なエンコード、チャンクの種類を**MIRACAST\_チャンク\_型\_エンコード\_完了**:  
示すこと、H.264 エンコードが完了しました。 **ProcessingTime**と**EncodeRate**のメンバー、 [ **DXGK\_MIRACAST\_チャンク\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-dxgk_miracast_chunk_info)構造体を完了する必要があります。

<span id="Frame_send__calling_ReportStatistic_using_MIRACAST_STATISTIC_TYPE_CHUNK_SENT_"></span><span id="frame_send__calling_reportstatistic_using_miracast_statistic_type_chunk_sent_"></span><span id="FRAME_SEND__CALLING_REPORTSTATISTIC_USING_MIRACAST_STATISTIC_TYPE_CHUNK_SENT_"></span>フレームの送信、呼び出す[ **ReportStatistic** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_report_statistic)を使用して**MIRACAST\_統計\_型\_チャンク\_SENT**:  
このフレーム/部品番号のデータ パケットが Miracast ユーザー モード ドライバーから転送用ネットワーク API に送信することを示します。 複数のネットワーク API 呼び出しを使用してこのフレーム/部分のデータを送信すると場合、しこれのみをログする最初のパケットが送信される直前に これを示すための呼び出しは、ネットワーク API を呼び出す直前に行われます。 これは、機能は、ネットワーク API を呼び出すと場合、したくないそのブロック時間のグラフィックス スタックのフレームの処理に対してカウントするので重要です。

<span id="Dropped_frame__chunk_type__MIRACAST_CHUNK_TYPE_FRAME_DROPPED_"></span><span id="dropped_frame__chunk_type__miracast_chunk_type_frame_dropped_"></span><span id="DROPPED_FRAME__CHUNK_TYPE__MIRACAST_CHUNK_TYPE_FRAME_DROPPED_"></span>フレームのドロップ、チャンクの種類**MIRACAST\_チャンク\_型\_フレーム\_ドロップ**:  
場合は、いつでも、ドライバーには、フレーム/パーツの処理を完了し、シンクに送信、ことはありませんが決定したら、ドロップしたフレームを報告する必要があります。 このコンテキストで、フレームにのみ考慮されます、ドライバーが実際にログインして処理を開始する場合は削除**MIRACAST\_チャンク\_型\_フレーム\_開始**します。 ドライバーは処理されず、このフレームをスキップすることをログに記録を計算します場合**MIRACAST\_チャンク\_型\_フレーム\_ドロップ**ログインしなくても **。MIRACAST\_チャンク\_型\_フレーム\_開始**します。

<span id="Driver_defined_chunk_type_MIRACAST_CHUNK_TYPE_ENCODE_DRIVER_DEFINED_1_or__2_"></span><span id="driver_defined_chunk_type_miracast_chunk_type_encode_driver_defined_1_or__2_"></span><span id="DRIVER_DEFINED_CHUNK_TYPE_MIRACAST_CHUNK_TYPE_ENCODE_DRIVER_DEFINED_1_OR__2_"></span>ドライバーには、チャンクの種類が定義されている**MIRACAST\_チャンク\_型\_エンコード\_ドライバー\_定義\_1**または **\_2**:  
これらのチャンクの型のシナリオのパフォーマンスの理解に役立つ利用できます。 ドライバーがこれらの型を使用してこのフレームの I フレームが作成されたことを示す例となります。 別の例は、フレームの最後のスライスがネットワークでエンコードされたフレームの合計サイズに含まれている Api に送信された後に、ドライバーが追加のパケットにログオンする場所になります。

フレームの色を変換する方法と、ディスプレイのミニポート ドライバーが、色変換の完了を報告する方法の例を示します。

**スライスを使用せずには、1 つのフレームをレポートします。**

値[ **MIRACAST\_チャンク\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/ns-netdispumdddi-miracast_chunk_info)メンバー。**ChunkType**値**ChunkId**します。
**ChunkId**します。
MIRACAST の処理のステージ\_チャンク\_型\_FrameNumber PartNumber ProcessingTime EncodeRate 開始処理フレーム**フレーム\_開始**101 0 0 0 色変換には完全な**色\_変換\_** **完了**101 0 950 0 エンコードが完了したら**エンコード\_** **完了**101 0 1042 15000 ネットワークにデータを送信する呼び出しの直前[ **ReportStatistic** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_report_statistic)呼び出す\*の値が 101、 **ChunkSent**. **ChunkId**します。 **FrameNumber**の値が 0 の場合、 **ChunkSent**します。 **ChunkId**します。 **PartNumber** N/A 該当なし
 

\*使用して呼び出す**MIRACAST\_統計\_型\_チャンク\_SENT**します。

**スライスを使用して処理を 1 つのフレームをレポートするには。**

値[ **MIRACAST\_チャンク\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/ns-netdispumdddi-miracast_chunk_info)メンバー。**ChunkType**
**ChunkId**します。
**ChunkId**します。
MIRACAST の処理のステージ\_チャンク\_型\_FrameNumber PartNumber ProcessingTime EncodeRate 開始処理フレーム**フレーム\_開始**101 0 0 0 色変換には完全な**色\_変換\_** **完了**101 0 950 スライス 1 の 0 のエンコードが完了したら**エンコード\_** **完全な**スライス 2 のエンコードが 101 1 1042 15000 完了**エンコード\_** **完了**101 0 400 15000をネットワークに1つのデータをスライスする送信への呼び出しの直前[ **ReportStatistic** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_report_statistic)呼び出す\*の値が 101、 **ChunkSent**します。 **ChunkId**します。 **FrameNumber**の値を 1、 **ChunkSent**します。 **ChunkId**します。 **PartNumber** N/A N/A だけを送信する呼び出しの前にネットワークに 2 つのデータをスライス[ **ReportStatistic** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_report_statistic)呼び出す\*の値が 101、 **ChunkSent**します。 **ChunkId**します。 **FrameNumber**の値が 0 の場合、 **ChunkSent**します。 **ChunkId**します。 **PartNumber** (上記の注を参照してください)。該当なしの該当なし
 

\*使用して呼び出す**MIRACAST\_統計\_型\_チャンク\_SENT**します。

**元のフレームをレポートして、処理、スライスを使用しないで再エンコードします。**

値[ **MIRACAST\_チャンク\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/ns-netdispumdddi-miracast_chunk_info)メンバー。**ChunkType**
**ChunkId**します。
**ChunkId**します。
MIRACAST の処理のステージ\_チャンク\_型\_FrameNumber PartNumber ProcessingTime EncodeRate 開始処理フレーム**フレーム\_開始**101 0 0 0 色変換には完全な**色\_変換\_** **完了**101 0 950 0 エンコードが完了したら**エンコード\_** **完了**101 0 1042 15000 元のフレームにデータをネットワークに送信するための呼び出しの直前[ **ReportStatistic** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_report_statistic)呼び出す\*の値が 101、 **ChunkSent**します。 **ChunkId**します。 **FrameNumber**の値が 0 の場合、 **ChunkSent**します。 **ChunkId**します。 **PartNumber** N/A N/A 再エンコードが完了したら**エンコード\_** **完了**101 0 500 15000 再エンコードされたフレームにデータをネットワークに送信するための呼び出しの直前[ **ReportStatistic** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_report_statistic)呼び出す\*の値が 101、 **ChunkSent**します。 **ChunkId**します。 **FrameNumber**の値が 0 の場合、 **ChunkSent**します。 **ChunkId**します。 **PartNumber** N/A 該当なし
 

\*使用して呼び出す**MIRACAST\_統計\_型\_チャンク\_SENT**します。

## <a name="span-idreportingprotocoleventsspanspan-idreportingprotocoleventsspanspan-idreportingprotocoleventsspanreporting-protocol-events"></a><span id="Reporting_protocol_events"></span><span id="reporting_protocol_events"></span><span id="REPORTING_PROTOCOL_EVENTS"></span>レポートのプロトコル イベント


Miracast ユーザー モード ドライバーが呼び出すことによってプロトコル イベントを報告すると、 [ **ReportStatistic** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_report_statistic)関数と[ **MIRACAST\_統計\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/ns-netdispumdddi-miracast_statistic_data).**StatisticType**設定**MIRACAST\_統計\_型\_イベント**、オペレーティング システムで、イベント ログに記録が他の処理を行いません。 これらのイベントは診断とパフォーマンスの調査を行うのに役立ちます。

[ **MIRACAST\_プロトコル\_イベント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/ne-netdispumdddi-miracast_protocol_event)列挙には可能なプロトコル イベントの種類報告できるにはが含まれています。

## <a name="span-idreportingprotocolerrorsspanspan-idreportingprotocolerrorsspanspan-idreportingprotocolerrorsspanreporting-protocol-errors"></a><span id="Reporting_protocol_errors"></span><span id="reporting_protocol_errors"></span><span id="REPORTING_PROTOCOL_ERRORS"></span>プロトコル エラーの報告


Miracast が接続されているセッションの進行中は、Miracast ユーザー モード ドライバーにエラーが検出された場合を呼び出す必要が、 [ **ReportSessionStatus** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_report_session_status)で適切なコールバック関数を[**MIRACAST\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/ne-netdispumdddi-miracast_status)でエラー状態の情報、 *MiracastStatus*パラメーター。 動作のセッションには、常にエラーが報告されたときに、セッションが破棄されます。

オペレーティング システムはログだけでは、 [ **ReportSessionStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_report_session_status)*状態*診断用のパラメーターをその値に基づいてアクションを受け取りません。 ただし、ドライバーがエラーの原因を区別するためにこのパラメーターを使用することをお勧めします。

 

 





