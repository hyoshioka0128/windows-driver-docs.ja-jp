---
title: サマリー メッセージ ファイル
description: サマリー メッセージ ファイル
ms.assetid: 90d82aee-5836-4f69-8e52-48400e1445cc
keywords:
- Tracefmt WDK、概要メッセージ ファイル
- 概要メッセージ ファイルの WDK Tracefmt
- WDK Tracefmt ファイル
- .sum ファイル
- 合計ファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9dce1d04a7dc1035e0959339aa2e7ff86dde467f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360938"
---
# <a name="summary-message-file"></a>サマリー メッセージ ファイル


## <span id="ddk_summary_message_file_tools"></span><span id="DDK_SUMMARY_MESSAGE_FILE_TOOLS"></span>


概要メッセージ ファイルは、ソフトウェア トレースに関する情報を含むテキスト ファイルです。 Tracefmt を作成、*概要メッセージ (.sum) ファイル*トレース ログにメッセージを処理またはセッションのトレースの後にします。

概要メッセージ ファイルには、統計サマリーで、次のデータが含まれます。

-   処理されるバッファーの数

-   メッセージの数が処理され、失われました。

-   経過時間 (マイクロ秒)、トレース セッションの

次の統計情報の要約は、トレースで表される各トレース メッセージの 1 つの行で構成されるテーブルです。 テーブルの各列は、トレース メッセージの詳細については、次の情報を提供します。

<span id="EventCount"></span><span id="eventcount"></span><span id="EVENTCOUNT"></span>**EventCount**  
トレースにトレース メッセージのインスタンスの数。

<span id="EventName"></span><span id="eventname"></span><span id="EVENTNAME"></span>**EventName**  
フレンドリ名、 [GUID をメッセージ](message-guid.md)トレース メッセージ。 既定では、メッセージの GUID のフレンドリ名には、トレース プロバイダーが作成されたディレクトリの名前が使用して別の表示名を指定することができます、 **-p**実行するようにパラメーター\_WPP または Tracewpp.exe します。 については、実行を参照してください。\_WPP オプション。 (**EventName** %1 の変数と同じ値を持つ、[トレース メッセージのプレフィックス](trace-message-prefix.md))。

<span id="EventType"></span><span id="eventtype"></span><span id="EVENTTYPE"></span>**イベントの種類**  
トレース メッセージのフレンドリ名。 既定では、トレース メッセージの表示名は、ソース ファイルとトレース メッセージを生成したコードの行番号の名前です。 (**EventType** %2 の変数と同じ値を持つ、[トレース メッセージのプレフィックス](trace-message-prefix.md))。

<span id="GUID"></span><span id="guid"></span>**GUID**  
メッセージ トレース メッセージの GUID。

次の例では、Tracedrv、トレース用にインストルメント化サンプル ドライバーによって生成される testtrace.etl トレース ログの概要メッセージ ファイルを示します。 [TraceDrv](https://go.microsoft.com/fwlink/p/?LinkId=617726)、ソフトウェア トレースのように設計されたドライバーのサンプルは、 [Windows ドライバー サンプル](https://go.microsoft.com/fwlink/p/?LinkId=616507)GitHub リポジトリにあります。

```
Files Processed:
d:\DDK Tools\tracetools\testtrace.etl
Total Buffers Processed 4
Total Events  Processed 1718
Total Events  Lost      4
Elapsed Time            122 sec
+---------------------------------------------------------------------------------+
|EventCount    EventName    EventType         Guid                                |
+---------------------------------------------------------------------------------+
|         1    Header       Header            68fdd900-4a3e-11d1-84f4-0000f80464e3|
|      1700    tracedrv     tracedrv_c264     37753236-c81f-505e-d40a-128d3bb2b5ff|
|        17    tracedrv     tracedrv_c258     37753236-c81f-505e-d40a-128d3bb2b5ff|
+---------------------------------------------------------------------------------+
```

Tracedrv がヘッダー メッセージおよび 2 つのトレース メッセージが生成される前の概要を示しています。 によって 1 つのトレース メッセージが生成された、 [ **DoTraceMessage** ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85)) 264 の行と、その他のステートメントは行 258 DoTraceMessage ステートメントによって生成されます。 このトレース ログには、最初のトレース メッセージの場合は 1700 インスタンスと 2 つ目のトレース メッセージのインスタンス数は 17 があります。

概要メッセージ ファイルはソフトウェアのトレースをデバッグするには、主に使用され、その形式が変更される可能性が。

 

 





