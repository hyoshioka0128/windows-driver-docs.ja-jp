---
title: サマリー メッセージ ファイル
description: サマリー メッセージ ファイル
ms.assetid: 90d82aee-5836-4f69-8e52-48400e1445cc
keywords:
- Tracefmt WDK、概要メッセージファイル
- 概要メッセージファイル WDK Tracefmt
- ファイル WDK Tracefmt
- . sum ファイル
- 合計ファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 785baa8f875ea0567ec22bcbaf8b1b5621f2a785
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769714"
---
# <a name="summary-message-file"></a>サマリー メッセージ ファイル


## <span id="ddk_summary_message_file_tools"></span><span id="DDK_SUMMARY_MESSAGE_FILE_TOOLS"></span>


概要メッセージファイルは、ソフトウェアトレースに関する情報を含むテキストファイルです。 Tracefmt は、トレースログまたはトレースセッションでメッセージを処理した後に、*概要メッセージ (. sum) ファイル*を作成します。

概要メッセージファイルには、統計概要に次のデータが含まれています。

-   処理されたバッファーの数

-   処理されて失われたメッセージの数

-   トレースセッションの経過時間 (マイクロ秒)

統計の概要に従うと、トレースで表されるトレースメッセージごとに1つの行で構成されるテーブルになります。 テーブルの各列には、トレースメッセージに関する次の情報が表示されます。

<span id="EventCount"></span><span id="eventcount"></span><span id="EVENTCOUNT"></span>**EventCount**  
トレース内のトレースメッセージのインスタンスの数。

<span id="EventName"></span><span id="eventname"></span><span id="EVENTNAME"></span>**EventName**  
トレースメッセージの[メッセージ GUID](message-guid.md)のフレンドリ名。 既定では、メッセージ GUID のフレンドリ名は、トレースプロバイダーがビルドされたディレクトリの名前ですが、 **-p**パラメーターを使用して、 \_ Wpp または TRACEWPP を実行することで、別のフレンドリ名を指定できます。 詳細については、「実行する WPP オプション」を参照してください \_ 。 (**EventName**には、[トレースメッセージプレフィックス](trace-message-prefix.md)の %1 変数と同じ値が指定されています)。

<span id="EventType"></span><span id="eventtype"></span><span id="EVENTTYPE"></span>**EventType**  
トレースメッセージのフレンドリ名。 既定では、トレースメッセージの表示名は、ソースファイルの名前と、トレースメッセージを生成したコードの行番号です。 (**EventType**の値は、[トレースメッセージのプレフィックス](trace-message-prefix.md)の %2 変数と同じです)。

<span id="GUID"></span><span id="guid"></span>**GUID**  
トレースメッセージのメッセージ GUID。

次の例は、トレース用にインストルメント化されたサンプルドライバーである Tracedrv によって生成される testtrace .etl トレースログの概要メッセージファイルを示しています。 ソフトウェアトレース用に設計された[Tracedrv](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/tracing/tracedriver)は、GitHub の[Windows ドライバーサンプル](https://github.com/Microsoft/Windows-driver-samples)リポジトリから入手できます。

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

前の概要では、Tracedrv がヘッダーメッセージと2つのトレースメッセージを生成することを示しています。 264行目の[**DoTraceMessage**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85))ステートメントによって1つのトレースメッセージが生成され、もう一方は258行目の DoTraceMessage ステートメントによって生成されます。 このトレースログには、最初のトレースメッセージのインスタンス1700と2番目のトレースメッセージの17個のインスタンスがあります。

概要メッセージファイルは、主にソフトウェアのトレースをデバッグするために使用され、その形式は変更される可能性があります。

 

 





