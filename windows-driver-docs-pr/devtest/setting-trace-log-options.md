---
title: トレース ログ オプションの設定
description: トレース ログ オプションの設定
ms.assetid: 3790a3af-69bd-4ccc-a116-0df6312f378a
keywords:
- 概要メッセージ WDK traceview でをファイルします。
- WDK のメッセージ ファイルの一覧
- トレース ログは、WDK traceview で、オプションの設定
- ログ ファイル WDK traceview で、オプションの設定
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ade6590e6fd373ae9d21d6f7f849ad15e2f0482
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530379"
---
# <a name="setting-trace-log-options"></a>トレース ログ オプションの設定


トレース ログを表示する場合は、リスティング ファイルまたは概要ファイルを作成することもできます。 これらのテキスト ファイルを表示し、ログ データを簡単に操作できます。 トレース ログのオプションを設定するには、次の手順を使用します。

1.  **ファイル** メニューのをクリックして**既存のログ ファイルを開く**します。

2.  **ログ ファイルの選択**] ダイアログ ボックスで、**ログ ファイルのオプション**領域で、[トレース ログのオプション。

次の一覧には、トレース ログのオプションについて説明します。

<span id="Create_Listing_File"></span><span id="create_listing_file"></span><span id="CREATE_LISTING_FILE"></span>**リスティング ファイルを作成します。**  
リアルタイムのトレース セッションから、トレース メッセージの書式設定された、読み取り可能なテキスト ファイルのバージョンを作成します。 または、[トレース ログ](trace-log.md)します。

関連付けられているテキスト ボックスで、リスティング ファイルのパスとファイル名を入力します。 既定値は"LogSession*N*"ここで、 *N*セッションが作成された順序を表す 0 から始まる整数します。

<span id="Create_Summary_File"></span><span id="create_summary_file"></span><span id="CREATE_SUMMARY_FILE"></span>**概要ファイルを作成します。**  
リアルタイムのトレース セッションやトレース ログの統計情報のテキスト ファイルを生成します。

関連付けられているテキスト ボックスで、概要ファイルのパスとファイル名を入力します。 既定値は"LogSession*N*"ここで、 *N*セッションが作成された順序を表す 0 から始まる整数します。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

既存のリストまたは概要ファイルを指定する場合、traceview では、警告なしのファイルを上書きします。

Traceview では、トレース セッションを停止すると、概要ファイルを作成します。 Traceview でウィンドウを閉じるには、トレース セッションを停止する前に場合、traceview では、セッションの概要ファイルを作成できません。

 

 





