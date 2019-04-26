---
title: トレース ログのテキスト バージョンの作成
description: トレース ログのテキスト バージョンの作成
ms.assetid: 15d15da3-e381-4b5f-81f2-300aa87e11db
keywords:
- Traceview で WDK、テキスト バージョンのトレース ログ
- トレース ログは、WDK traceview で、テキストのバージョン
- ログ ファイル WDK traceview で、テキストのバージョン
- トレース メッセージの一覧 WDK
- テキスト形式のトレース ログは、WDK
- WDK ソフトウェア トレースのファイルを一覧表示します。
- .out ファイル
- ファイルを
- トレース ログの形式に変換します。
- WDK のオーディオ、トレース ログを形式します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb57c669a68a71656e5e7cb1a40ac6ffa517d60d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356634"
---
# <a name="creating-text-versions-of-trace-logs"></a>トレース ログのテキスト バージョンの作成


トレース ログ セッション中に生成されるトレース メッセージは保存[トレース ログ](trace-log.md)大量のトレース メッセージを効率的に格納するように設計されたバイナリ ファイルであります。 Traceview では、これらのファイルの人間が判読できるバージョンを作成するためのいくつかの便利なメソッドがあります。

### <a name="span-idcreatingalistingfileforarealtimetracesessionspanspan-idcreatingalistingfileforarealtimetracesessionspancreating-a-listing-file-for-a-real-time-trace-session"></a><span id="creating_a_listing_file_for_a_real_time_trace_session"></span><span id="CREATING_A_LISTING_FILE_FOR_A_REAL_TIME_TRACE_SESSION"></span>リアルタイムのトレース セッションのリスティング ファイルを作成します。

**リスティング ファイルの作成**オプションを作成、*リスティング ファイル*(.out)、セッション中に生成されるすべてのトレース メッセージのテキスト ファイル。 トレース セッションを作成するときにのみこのオプションを使用することができます。 リスティング ファイルのリアルタイムのトレース セッションを作成するには、次の操作を行います。

1.  **ファイル**メニューの  **Create New Log Session**します。

2.  プロバイダーを追加し、クリックして**次**します。

3.  **ログ セッション オプション**] ページで [**ログ セッション オプションの高度な**します。

4.  **出力ファイル**] タブで [**リスティング ファイルの作成**です。

詳細については、次を参照してください[トレース セッション オプションの詳細設定。](setting-advanced-trace-session-options.md)

### <a name="span-idcreatingalistingfileforanexistinglogfilespanspan-idcreatingalistingfileforanexistinglogfilespancreating-a-listing-file-for-an-existing-log-file"></a><span id="creating_a_listing_file_for_an_existing_log_file"></span><span id="CREATING_A_LISTING_FILE_FOR_AN_EXISTING_LOG_FILE"></span>既存のログ ファイルの一覧ファイルを作成します。

トレースのログ セッションを開始するには、中に使用することができます、**リスティング ファイルの作成**トレース ログのテキスト バージョンを作成するオプション。 既存のログ ファイルのリスティング ファイルを作成するには、次の操作を行います。

1.  **ファイル** メニューのをクリックして**既存のログ ファイルを開く**します。

2.  **ログ ファイルの選択**ダイアログ ボックスで、**リスティング ファイルの作成**です。

3.  **ログ ファイル名**ボックスで、既存のイベント トレース ログ (.etl) ファイルの名前を指定します。

トレース ログを表示する場合、traceview では、リスティング ファイルを作成します。 詳細については、次を参照してください。[トレース ログ オプションの設定](setting-trace-log-options.md)します。

詳細については、次を参照してください。 [ **traceview で-プロセス**](traceview--process.md)します。

### <a name="span-idcopyingthetracemessagelistspanspan-idcopyingthetracemessagelistspan-copying-the-trace-message-list"></a><span id="copying_the_trace_message_list"></span><span id="COPYING_THE_TRACE_MESSAGE_LIST"></span> トレース メッセージの一覧をコピー

トレース メッセージは、既存のトレース ログまたは実行中のトレース セッションのトレース メッセージの一覧から直接コピーできます。

この手順では、表示を細かく制御をできます。 後のメッセージをコピーする[トレース セッションをグループ化](grouping-trace-sessions.md)、表示する列 (つまり、トレース メッセージのプロパティ) を選択し、並べ替えおよびトレース メッセージをフィルター処理します。 表示から、個々 のメッセージを選択することもできます。 トレース メッセージの一覧からトレース メッセージをコピーするには、次の操作を行います。

1.  コピーするトレース メッセージを選択します。 Shift キーを押しながらクリックを使用すると、連続していないメッセージをコピーするのにには、連続するメッセージまたは ctrl キーを押しながらクリックを選択します。

2.  Ctrl キーを押しながら C キーを押します。 または、選択したメッセージの任意のセルを右クリックし、クリックして**コピー**します。

メッセージは、タブ区切り形式でコピーされます。 テキスト ファイルまたは保存するためのスプレッドシート ファイルに貼り付けることができ、分析します。
