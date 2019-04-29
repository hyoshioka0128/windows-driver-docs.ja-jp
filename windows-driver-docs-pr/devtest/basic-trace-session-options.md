---
title: トレース セッションの基本オプション
description: トレース セッションの基本オプション
ms.assetid: c997310f-79dc-4c94-945e-13a0a7786928
keywords:
- WDK、基本的なオプションのセッションをトレースします。
- トレース WDK、基本的なオプション
- ソフトウェアの WDK、基本的なオプションのトレース
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 042d6252918efb7dc3755333855eefe354ab138a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330962"
---
# <a name="basic-trace-session-options"></a>トレース セッションの基本オプション

次に示します、基本的なトレース セッション オプションに変更できる、**ログ セッション オプション**ページ。

<span id="Real_Time_Display"></span><span id="real_time_display"></span><span id="REAL_TIME_DISPLAY"></span>**リアルタイム表示**  
作成、[リアルタイム トレース セッション](trace-session.md#ddk_real_time_trace_sessions_tools)します。既定では、このオプションを選択します。

選択する必要があります**ログ トレース イベント データをファイルにリアルタイム表示**、またはその両方です。

<span id="Log_Session_Name"></span><span id="log_session_name"></span><span id="LOG_SESSION_NAME"></span>**ログ セッション名**  
トレース セッションの名前を指定します。 最大 1024 文字までの Windows 名前付け基準を満たしている任意の名前を選択します。 既定値は"LogSession*N*"ここで、 *N*セッションが作成された順序を表す 0 から始まる整数します。

その名前で、セッションを参照することができますトレース セッションの名前を付けた後 (たとえば、使用する場合、 [traceview でコマンド ライン インターフェイス](traceview-command-line-interface.md))。

<span id="Log_Trace_Event_Data_To_File__"></span><span id="log_trace_event_data_to_file__"></span><span id="LOG_TRACE_EVENT_DATA_TO_FILE__"></span>**ログ トレースのイベント データをファイル**   
作成、[トレース ログ セッション](trace-session.md#ddk_trace_log_sessions_tools)します。

選択する必要があります**ログ トレース イベント データをファイル**、**リアルタイム表示**、またはその両方です。

<span id="Log_File_Name"></span><span id="log_file_name"></span><span id="LOG_FILE_NAME"></span>**ログ ファイルの名前**  
パスとファイル名を指定します、[トレース ログ](trace-log.md)(.etl)。 このオプションが有効になっている場合にのみ、**ログ トレース イベント データをファイル**オプションを選択します。

既定でトレース ログの名前は"LogSession<em>\_日付\_時間</em>.etl"、ローカル ディレクトリに保存されます。 名前または場所を変更するには、テキスト ボックスにパスとファイル名を入力するか、ディレクトリに移動するでは、省略記号ボタン (…) をクリックします。

> [!CAUTION]
> 既存のファイルの名前とパスを選択した場合、traceview では、警告なしには、そのファイルを上書きします。

<span id="Append_To_Existing_Log_File"></span><span id="append_to_existing_log_file"></span><span id="APPEND_TO_EXISTING_LOG_FILE"></span>**既存のログ ファイルに追加します。**  
指定されているトレース ログ ファイルの末尾に、トレース メッセージを追加、**ログ ファイル名**ボックスで、ファイルを上書きする代わりにします。

このオプションが有効になっている場合にのみ**ログ トレース イベント データをファイル**が有効になっていると**リアルタイム表示**は無効です。 既存のトレース ログにリアルタイムのイベントを追加することはできません。

Traceview で指定されたファイルがまだ存在しない場合でも、このオプションを選択できます。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

トレース ログ (.etl) ファイル、traceview では、出力ファイルまたは traceview で概要ファイル、トレース セッションの名前は、イベントの保存されません。 Traceview でを使用してトレース ログを表示するときに、既定のセッション名を使用して"LogSession*N*"、トレース セッションの名前と場所*N*順序を表す 0 から始まる整数が、セッションが作成されます。
