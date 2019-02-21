---
title: Traceview でエラーを解決します。
description: Traceview でエラーを解決します。
ms.assetid: 4849e0b6-5dc9-4666-b1ca-ec89cb94bed0
keywords:
- Traceview で WDK、エラー
- WDK traceview でのエラー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d82be9f0bf8de5bd34c786ff6a60c4809e9d9c4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557803"
---
# <a name="resolving-traceview-errors"></a>Traceview でエラーを解決します。

このトピックでは、エラー traceview でよくレポートし、解決策を提案について説明します。 トラブルシューティングの完全なガイドを使用するものではありません。

### <a name="span-idtraceproviderisnotaddedspanspan-idtraceproviderisnotaddedspantrace-provider-is-not-added"></a><span id="trace_provider_is_not_added"></span><span id="TRACE_PROVIDER_IS_NOT_ADDED"></span>トレース プロバイダーは追加されません。

Traceview でが見つからない場合、 [PDB シンボル ファイル](pdb-symbol-files.md)または[トレース メッセージの形式 (.tmf) ファイル](trace-message-format-file.md)トレース プロバイダーの追加しないトレース プロバイダーのプロバイダーの一覧に、**新しいログ セッションの作成**ダイアログ ボックスで、また、プロバイダーを追加したいない理由を説明するメッセージを表示しません。

プロバイダーの一覧に追加して、手順を再開した後で、プロバイダーが表示されない場合、**形式情報ソースを選択します**ダイアログ ボックスで、をクリックして**TMF ファイルの選択**ではなく**TMF 検索パスを設定**します。 プロバイダーは、PDB ファイルまたは TMF ファイルを見つけられない、プロバイダーとトレース セッションを作成する traceview でを使うことはできません。

### <a name="span-idfailedtoenabletraceforcontrolguidguidspanspan-idfailedtoenabletraceforcontrolguidguidspanfailed-to-enable-trace-for-control-guid-guid"></a><span id="failed_to_enable_trace_for_control_guid__guid"></span><span id="FAILED_TO_ENABLE_TRACE_FOR_CONTROL_GUID__GUID"></span>コントロールの GUID のトレースを有効にできませんでした: *guid*

このエラーは、通常、1 つ以上のトレース コンシューマーは、システム上で 1 つのトレース プロバイダーからイベントを収集するがときに発生します。 この競合を解決するには、コンピューター上で実行され、競合しているセッションを停止するすべてのトレース セッションを表示します。

コマンド プロンプト ウィンドウで、コンピューター上のすべてのトレース セッションを表示する次のように入力します。 **traceview で-l**します。 (Traceview でウィンドウに traceview で実行されているトレース セッションのみが表示されます)。結果の表示には、アクティブなセッションが一覧表示します。

コマンド プロンプト ウィンドウで、トレース セッションを停止する次のように入力します。 **traceview で-停止 * * * SessionName*します。

これらのコマンドの詳細については、次を参照してください。 [ **traceview で管理コマンド**](traceview-control-commands.md)します。

### <a name="span-idcannotopenlogfileforreadingspanspan-idcannotopenlogfileforreadingspancannot-open-logfile-for-reading"></a><span id="cannot_open_logfile_for_reading"></span><span id="CANNOT_OPEN_LOGFILE_FOR_READING"></span>読み取り用のログ ファイルを開くことができません。

このエラーは、ログに traceview でリアルタイムのトレース セッションまたは別の既存のトレース イベントを提供しているトレース プロバイダーの既存のトレース ログを表示するときに発生します。

### <a name="span-idcannotconnecttoanytracesessioninthegroupspanspan-idcannotconnecttoanytracesessioninthegroupspancannot-connect-to-any-trace-session-in-the-group"></a><span id="cannot_connect_to_any_trace_session_in_the_group"></span><span id="CANNOT_CONNECT_TO_ANY_TRACE_SESSION_IN_THE_GROUP"></span>グループ内の任意のトレース セッションに接続できません。

このエラーを解決するには、確認、[グループ化の制限事項](limitations-of-grouping.md)トピックされ、システムにグループ化できるトレース セッションのみが含まれます。

### <a name="span-idinternalerrorclosetraceerror170spanspan-idinternalerrorclosetraceerror170spaninternal-error-closetrace-error-170"></a><span id="internal_error__closetrace_error_170"></span><span id="INTERNAL_ERROR__CLOSETRACE_ERROR_170"></span>内部エラー:CloseTrace エラー 170

このエラーは、既に進行中である NT Kernel Logger トレース セッションに参加するときに発生します。 Traceview でを使用して、NT Kernel Logger のトレース セッションを作成することができますが、ツールまたは traceview で以外の方法によって開始される NT Kernel Logger トレース セッションに参加することはできません。

詳細については、次を参照してください。[トレース セッションに参加する](joining-a-trace-session.md)と[NT Kernel Logger のトレース セッションを作成する](creating-an-nt-kernel-logger-trace-session.md)します。
