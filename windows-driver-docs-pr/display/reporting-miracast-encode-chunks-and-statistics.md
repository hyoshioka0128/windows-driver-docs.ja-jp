---
title: Miracast エンコードのチャンクおよび統計情報のレポート
description: ディスプレイハードウェアは、フレームを複数の部分に分割するか、チャンクをエンコードすることによって、Miracast ワイヤレス表示リンクを介して送信された各ビデオフレームを処理できます。
ms.assetid: E1CE637F-42ED-4BEB-A2FF-04B4B88469DC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2379210e7f533c86859aa156b329351202432ca3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825938"
---
# <a name="reporting-miracast-encode-chunks-and-statistics"></a>Miracast エンコードのチャンクおよび統計情報のレポート


ディスプレイハードウェアは、フレームを複数の部分に分割するか、*チャンクをエンコード*することによって、Miracast ワイヤレス表示リンクを介して送信された各ビデオフレームを処理できます。 各チャンクには、フレーム番号とフレームパーツ (またはスライス) 番号から生成された一意のチャンク ID があります。 同じデスクトップのフレーム更新に関連付けられている各チャンクには、同じフレーム番号を割り当てる必要があります。

## <a name="span-idreporting_chunk_processingspanspan-idreporting_chunk_processingspanspan-idreporting_chunk_processingspanreporting-chunk-processing"></a><span id="Reporting_chunk_processing"></span><span id="reporting_chunk_processing"></span><span id="REPORTING_CHUNK_PROCESSING"></span>チャンク処理のレポート


ドライバーでは、複数の処理手順 (エンコードからのカラー変換の分離など) または単一の手順で、Miracast ワイヤレスリンクを介して送信されるようにフレームをエンコードできます。 各処理手順には、フレーム内に一意のフレームパーツ番号を割り当てる必要があります。

Miracast ユーザーモードドライバーまたはディスプレイミニポートドライバーは、ハードウェアがフレームの処理手順を完了するたび、およびフレームの各部分がネットワークに送信される直前に、オペレーティングシステムに通知する必要があります。 報告される特定の処理手順の時間は、オペレーティングシステムにイベントが報告された時刻と想定されているため、できるだけ迅速にステージを報告することが重要です。

オペレーティングシステムは、Windows イベントトレーシング (ETW) カーネルレベルのトレース機能を使用してこれらのイベントをログに記録する以外に、アクションを実行しません。 この情報は、パフォーマンスの問題の測定と調査にも重要です。

ドライバーが通知を提供するには、次の方法があります。

-   Miracast ユーザーモードドライバーは、 [**Reportstatistic**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_report_statistic)のコールバック関数を呼び出して、 **MIRACAST\_の統計\_型\_チャンク\_処理\_完全な**型、または miracast を使用して詳細を報告し **\_統計\_** は、チャンクが送信のためにネットワークスタックに送信されようとしていることを示すために送信されたチャンク\_\_の種類を示します。
-   表示ミニポートドライバーは、 **DXGK\_INTERRUPT\_MICACAST\_チャンク\_処理\_完全**な割り込みの種類を使用してチャンク処理の詳細を報告しますが、このレポートは割り込み時間にのみ作成できます。また、チャンク情報をログに記録することに加えて、チャンクパケットが作成され、キューに入れられます。これにより、Miracast ユーザーモードドライバーは[**GetNextChunkData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_get_next_chunk_data) callback 関数を呼び出すことによって取得できるようになります。
-   表示ミニポートドライバーは、任意の IRQL レベルで[**Dxgkcbreportchunkinfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_miracast_report_chunk_info)コールバック関数を呼び出します。 この関数はチャンク情報のみをログに記録します。チャンクパケットはキューに記録されません。

デスクトップイメージが更新されていないが、ドライバーがデスクトップイメージを再度エンコードして品質を向上させる必要がある場合は、同じフレーム番号とパーツ番号を使用する必要があります。 パフォーマンスツールは、同じフレームとパート番号に対して2番目のエンコード完了イベントをトリガーし、同じフレームの2番目のエンコードが実行されたことを示します。

**注**  各フレームの最後のスライスには、フレーム部分の0を指定する必要があります。 これは、パフォーマンスツールに対して、フレームの最後のスライスであることを示します。

 

プライマリサーフェイスが正しく同期されていることを確認するために、エンコードがピクセルパイプラインによって実行される場合は、エンコードがプライマリサーフェイスへのアクセスを終了する前に、垂直同期の間隔で要求されたフリップ操作を報告しないようにする必要があります。 これにより、エンコードエンジンが読み取りを行っているときに、プレゼンターがプライマリサーフェイスにレンダリングされるのを防ぐことができます。

Miracast ユーザーモードドライバーは、フレームを処理する複数のステージごとに、オペレーティングシステムに通知する必要があります。

<span id="Start_frame__chunk_type__MIRACAST_CHUNK_TYPE_FRAME_START_"></span><span id="start_frame__chunk_type__miracast_chunk_type_frame_start_"></span><span id="START_FRAME__CHUNK_TYPE__MIRACAST_CHUNK_TYPE_FRAME_START_"></span>開始フレーム、チャンクの種類**MIRACAST\_チャンク\_種類\_フレーム\_開始**:  
オペレーティングシステムが新しいデスクトップフレームを表示するようにドライバーに要求するポイントを表します。 これは、厳密には Miracast ユーザーモードドライバーから報告できますが、新しいフレームの処理の開始には常にミニポートドライバーが含まれ、そのドライバーによって報告される必要があります。

<span id="Color_convert_complete__chunk_type_MIRACAST_CHUNK_TYPE_COLOR_CONVERT_COMPLETE_"></span><span id="color_convert_complete__chunk_type_miracast_chunk_type_color_convert_complete_"></span><span id="COLOR_CONVERT_COMPLETE__CHUNK_TYPE_MIRACAST_CHUNK_TYPE_COLOR_CONVERT_COMPLETE_"></span>カラー変換完了、チャンクの種類**MIRACAST\_チャンク\_種類\_色\_変換\_完了**:  
一部のソリューションには、異なる色の変換とエンコードのステージがあります。 このようなソリューションでは、color convert complete processing イベントができるだけ早く報告される必要があり、ドライバーは[**DXGK\_MIRACAST\_チャンクの\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-dxgk_miracast_chunk_info)を使用する必要があります。**Processingtime**メンバーは、ハードウェアが操作を実行するためにかかった時間を報告します。 フレーム全体がスライスではなく一度にすべての色で変換された場合は、部品番号を0にする必要があります。

<span id="Encode_complete__chunk_type_MIRACAST_CHUNK_TYPE_ENCODE_COMPLETE_"></span><span id="encode_complete__chunk_type_miracast_chunk_type_encode_complete_"></span><span id="ENCODE_COMPLETE__CHUNK_TYPE_MIRACAST_CHUNK_TYPE_ENCODE_COMPLETE_"></span>エンコードの完了、チャンクの種類**MIRACAST\_チャンク\_型\_エンコード\_完了**します。  
H.264 エンコードが完了したことを示します。 [**DXGK\_MIRACAST\_チャンク\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-dxgk_miracast_chunk_info)構造体の**Processingtime**メンバーと**EncodeRate**メンバーを完了する必要があります。

<span id="Frame_send__calling_ReportStatistic_using_MIRACAST_STATISTIC_TYPE_CHUNK_SENT_"></span><span id="frame_send__calling_reportstatistic_using_miracast_statistic_type_chunk_sent_"></span><span id="FRAME_SEND__CALLING_REPORTSTATISTIC_USING_MIRACAST_STATISTIC_TYPE_CHUNK_SENT_"></span>フレーム送信、MIRACAST を使用した[**reportstatistic**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_report_statistic)の呼び出し **\_チャンク\_送信された\_の種類の統計\_** ます。  
このフレーム/パート番号のデータパケットが、Miracast ユーザーモードドライバーからの伝送のためにネットワーク API に送信されるだけであることを示します。 このフレーム/パートのデータが、ネットワーク API の複数の呼び出しを使用して送信された場合、最初のパケットが送信される直前にのみログを記録する必要があります。 の呼び出しは、ネットワーク API を呼び出す直前に行う必要があることを示しています。 これが重要なのは、ネットワーク API がを呼び出したときに、そのブロック時間がグラフィックススタック内のフレームの処理に対してカウントされないようにするためです。

<span id="Dropped_frame__chunk_type__MIRACAST_CHUNK_TYPE_FRAME_DROPPED_"></span><span id="dropped_frame__chunk_type__miracast_chunk_type_frame_dropped_"></span><span id="DROPPED_FRAME__CHUNK_TYPE__MIRACAST_CHUNK_TYPE_FRAME_DROPPED_"></span>フレームをドロップしました。チャンクの種類**MIRACAST\_チャンク\_種類\_フレーム\_削除**されました:  
ドライバーがフレーム/パーツの処理を完了せず、シンクに送信することを決定した場合は、ドロップされたフレームを報告する必要があります。 このコンテキストでは、フレームが削除されたと見なされるのは、ドライバーが MIRACAST\_\_チャンクをログに記録して実際に処理を開始した場合だけです。 **\_フレーム\_開始**します。 ドライバーが、このフレームを処理せずにスキップすることを計算した場合は、miracast をログに記録して **\_\_フレーム**をログに記録することができます。\_は、 **miracast\_チャンク\_型\_フレームにログを記録せずにドロップ\_ます。_ 開始**します。\_

<span id="Driver_defined_chunk_type_MIRACAST_CHUNK_TYPE_ENCODE_DRIVER_DEFINED_1_or__2_"></span><span id="driver_defined_chunk_type_miracast_chunk_type_encode_driver_defined_1_or__2_"></span><span id="DRIVER_DEFINED_CHUNK_TYPE_MIRACAST_CHUNK_TYPE_ENCODE_DRIVER_DEFINED_1_OR__2_"></span>ドライバーが定義されたチャンクの種類**MIRACAST\_チャンク\_型\_エンコード\_ドライバー\_定義\_1**または **\_2**:  
これらのチャンクの種類は、シナリオのパフォーマンスを理解するのに役立ちます。 例として、ドライバーがこれらの型を使用して、このフレームに対して I フレームが作成されたことを示します。 もう1つの例として、フレームの最後のスライスがエンコードされたフレームの合計サイズを含むネットワーク Api に送信された後に、ドライバーが追加のパケットをログに記録する場合があります。

ここでは、フレームの色を変換する方法の例を示し、ディスプレイミニポートドライバーがカラー変換の完了を報告する方法について説明します。

**スライスを使用せずに1つのフレームをレポートする:**

MIRACAST の値[ **\_チャンク\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdispumdddi/ns-netdispumdddi-miracast_chunk_info)メンバー: **Chunktype**値**ChunkId**。
**ChunkId**。
MIRACAST\_ チャンクの処理ステージ\_種類\_ FrameNumber PartNumber ProcessingTime EncodeRate 処理フレーム **\_フレーム**を開始します。 101 0 0 0 カラー変換が完了し、変換が完了し、**変換**\_**Complete** 101 0 950 0 encode は、Network [**reportstatistic**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_report_statistic)呼び出し\* 101、**送信された chunksent**値に対してデータを送信するための呼び出しの直前に、完全な**エンコード\_** **101 0 1042 15000 を**完了します。\_ **ChunkId**。 **FrameNumber** 0、sent の値が**送信さ**れました。 **ChunkId**。 **Partnumber**該当なし
 

\*MIRACAST\_統計を使用して呼び出され、**チャンク\_送信さ**れた\_の種類を\_します。

**スライスを使用して処理された1つのフレームのレポート:**

MIRACAST の値[ **\_チャンク\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdispumdddi/ns-netdispumdddi-miracast_chunk_info)メンバー: **Chunktype**
**ChunkId**。
**ChunkId**。
MIRACAST\_ チャンクの処理ステージ\_種類\_ FrameNumber PartNumber ProcessingTime EncodeRate 処理フレーム **\_フレーム**を開始します。 101 0 0 0 カラー変換が完了し、変換が完了し、**変換**\_**完了**101 0 950 0 スライス1のエンコードが完了しました。スライス1のデータを送信するための呼び出しの直前に、スライス 2**の完全な**エンコード 101 0 400 15000 **\_** **完全な**エンコードを完了し 101 1 1042 15000 **\_** network [**Reportstatistic**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_report_statistic)では、\* 101、値が**sent sent**の値が呼び出されます。\_ **ChunkId**。 **FrameNumber** 1、Sent of **chunksent**値。 **ChunkId**。 **Partnumber**スライス2データを network [**reportstatistic**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_report_statistic)に送信する直前に、n/a n/a が返されます。これは、\* 101 になりました。また、 **chunksent**の値です。 **ChunkId**。 **FrameNumber** 0、sent の値が**送信さ**れました。 **ChunkId**。 **Partnumber** (上のメモを参照してください。)該当なし
 

\*MIRACAST\_統計を使用して呼び出され、**チャンク\_送信さ**れた\_の種類を\_します。

**スライスを使用せずに、元のフレームを報告し、処理した後、再エンコードします。**

MIRACAST の値[ **\_チャンク\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdispumdddi/ns-netdispumdddi-miracast_chunk_info)メンバー: **Chunktype**
**ChunkId**。
**ChunkId**。
MIRACAST\_ チャンクの処理ステージ\_種類\_ FrameNumber PartNumber ProcessingTime EncodeRate 処理フレーム **\_フレーム**を開始します。 101 0 0 0 カラー変換が完了し、変換が完了し、**変換**\_**完全な**101 0 950 0 エンコードは、元のフレームのデータを Network [**reportstatistic**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_report_statistic)呼び出し\* 101、**送信された chunksent**値に送信するための呼び出しの直前に **、101 0 1042 15000 の完全な** **エンコード\_** ます。\_ **ChunkId**。 **FrameNumber** 0、sent の値が**送信さ**れました。 **ChunkId**。 **Partnumber**N/A N/A 再エンコードが完了するのは、再エンコードされたフレームのデータを送信する前に、再エンコードされたフレームのデータをネットワーク[**reportstatistic**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_report_statistic) 101 に送信する直前に **\_** 101 0 500 15000**完了**し、 **chunksent**の値です。\* **ChunkId**。 **FrameNumber** 0、sent の値が**送信さ**れました。 **ChunkId**。 **Partnumber**該当なし
 

\*MIRACAST\_統計を使用して呼び出され、**チャンク\_送信さ**れた\_の種類を\_します。

## <a name="span-idreporting_protocol_eventsspanspan-idreporting_protocol_eventsspanspan-idreporting_protocol_eventsspanreporting-protocol-events"></a><span id="Reporting_protocol_events"></span><span id="reporting_protocol_events"></span><span id="REPORTING_PROTOCOL_EVENTS"></span>プロトコルイベントの報告


Miracast ユーザーモードドライバーが、Miracast を使用して[**Reportstatistic**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_report_statistic)関数を呼び出すことによってプロトコルイベントを報告する場合[ **\_統計\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdispumdddi/ns-netdispumdddi-miracast_statistic_data)。**StatisticType**が MIRACAST\_に設定されています。 **\_の種類\_イベント**では、オペレーティングシステムはイベントをログに記録しますが、それ以外の操作は実行しません。 これらのイベントは、診断やパフォーマンスの調査にも役立ちます。

[**MIRACAST\_protocol\_イベント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdispumdddi/ne-netdispumdddi-miracast_protocol_event)列挙には、報告可能なプロトコルイベントの種類が含まれています。

## <a name="span-idreporting_protocol_errorsspanspan-idreporting_protocol_errorsspanspan-idreporting_protocol_errorsspanreporting-protocol-errors"></a><span id="Reporting_protocol_errors"></span><span id="reporting_protocol_errors"></span><span id="REPORTING_PROTOCOL_ERRORS"></span>プロトコルエラーの報告


Miracast 接続セッションが進行中であるときに、Miracast ユーザーモードドライバーがエラーを検出した場合、 *MiracastStatus*パラメーターの適切な[**miracast\_status**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdispumdddi/ne-netdispumdddi-miracast_status)エラー状態情報で[**reportsessionstatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_report_session_status)コールバック関数を呼び出す必要があります。 エラーが報告された場合、オペレーティングセッションは常にセッションを破棄します。

オペレーティングシステムは診断の[**Reportsessionstatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_report_session_status)*のパラメーターを*ログに記録するだけですが、その値に基づいて何のアクションも実行しないことに注意してください。 ただし、このパラメーターを使用して、エラーのさまざまな原因を区別することをお勧めします。

 

 





