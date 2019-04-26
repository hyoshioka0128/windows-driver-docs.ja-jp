---
title: トレース セッションへの参加
description: トレース セッションへの参加
ms.assetid: 0fd065e4-004f-426a-bdb1-4b2e7d219e20
keywords:
- トレース セッションに参加します。
- WDK、トレース、進行中のセッション
- 実行中のトレース セッション WDK
- ソフトウェア WDK をトレースするには、実行中のセッション
- トレース セッションを停止しています
- トレース セッションのキャンセル
- トレース セッションを再起動します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c39e5d0516054ab13dffff2e12705e20b23c92f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356510"
---
# <a name="joining-a-trace-session"></a>トレース セッションへの参加


Traceview でを実行中のトレース セッションを制御しているときに終了を強制するなどのまれな状況で、traceview でがいないセッション プロバイダーを無効にし、トレース セッションを停止しません。 このような状況でまだ有効になっているプロバイダーでトレース セッションを開始しようとすると traceview では警告を表示して停止して、セッションを再起動するかが既に進行中のトレース セッションに参加できるように提供しています。

ダイアログ ボックスのオプションは次のとおりです。

<span id="Yes_-_Stop_and_Restart_the_Log_Session"></span><span id="yes_-_stop_and_restart_the_log_session"></span><span id="YES_-_STOP_AND_RESTART_THE_LOG_SESSION"></span>**はい - 停止し、ログ セッションの再開**  
Traceview では、トレース セッションを停止し、同じプロバイダーと同じプロパティを持つ新しいトレース セッションを開始します。

<span id="No_-_Join_the_Log_Session_Without_Stopping"></span><span id="no_-_join_the_log_session_without_stopping"></span><span id="NO_-_JOIN_THE_LOG_SESSION_WITHOUT_STOPPING"></span>**いいえ - 停止することがなくログ セッションに参加します。**  
Traceview では、取得し、セッションのプロパティを保存し、トレース セッションに参加します。 Traceview でを使用して、トレース セッションのプロパティを変更することができますが、traceview では、トレース セッションを停止できません。 トレース セッションを停止する[traceview で終了](starting-and-exiting-traceview.md)します。

<span id="Cancel_-_Abort_Start_Operation"></span><span id="cancel_-_abort_start_operation"></span><span id="CANCEL_-_ABORT_START_OPERATION"></span>**[キャンセル] - 中止操作の開始**  
Traceview では、トレース セッションを開始する試行を取り消します。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

Traceview でウィンドウを起動してトレース セッションを実行しているものだけが表示されます。 システムで実行されているすべてのトレース セッションの一覧、入力**traceview で-l**コマンド プロンプト ウィンドウでします。 Traceview では開始されませんでしたトレース セッションを停止する次のように入力します。 **traceview で-停止 * * * SessionName*コマンド プロンプト ウィンドウでします。 これらのコマンドの詳細については、次を参照してください。 [traceview でコマンド ライン インターフェイス](traceview-command-line-interface.md)します。

 

 





