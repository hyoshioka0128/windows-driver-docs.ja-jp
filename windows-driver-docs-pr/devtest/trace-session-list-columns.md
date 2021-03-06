---
title: トレース セッション一覧の列
description: トレース セッション一覧の列
ms.assetid: 2e9d7636-3cff-459c-827a-719062bb778c
keywords:
- トレース セッションの WDK の一覧
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3f630ea21461e0bb84e124807440cf434833202
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354661"
---
# <a name="trace-session-list-columns"></a>トレース セッション一覧の列


内の列、[トレース セッション リスト](trace-session-list.md)トレース セッションと、トレース プロバイダーのプロパティを表します。 これらのプロパティのほとんどを設定することができます、[ログ セッションのパラメーター オプション](log-session-parameter-options.md)のタブ、**ログ セッション オプションの高度な**トレース セッションを作成するときに、ダイアログ ボックス。 オプションの詳細については、**ログ セッションのパラメーター オプション** タブを参照してください[トレース セッション オプションの高度な設定](setting-advanced-trace-session-options.md)します。

トレース セッションの実行中に変更できるプロパティは、黒色の文字が使用できる表示で表示されます。 トレース セッションが停止している場合にのみ変更可能なプロパティは、使用できなくなります。 トレース ログにトレース メッセージのプロパティを変更できません。 詳細については、次を参照してください。[トレース セッションのプロパティを変更する](changing-the-properties-of-a-trace-session.md)します。

次の一覧では、すべての既定で非表示になっているものも含め、トレース セッションの一覧で列について説明します。 非表示の列を表示する方法については、「列の非表示とを表示する」を参照してください[トレース セッション リスト機能](trace-session-list-features.md)します。

<span id="Group_ID___Session_Name"></span><span id="group_id___session_name"></span><span id="GROUP_ID___SESSION_NAME"></span>**グループ ID/セッション名**  
グループ ID とセッションの名前が表示されます。 この列を非表示にすることはできません。

**グループ ID** traceview では、トレース セッションに代入する識別子です。 トレース セッションのグループ内のトレース セッションを組み合わせると、traceview では、単一の識別子をグループに再度割り当てます。 値**グループ ID**の各ウィンドウ フレームにも表示されます[トレース メッセージ一覧](trace-message-lists.md)セッションにトレース メッセージをトレース セッションを関連付けることが役立つのです。

**セッション名**トレース セッションが作成されたときに割り当てた名前を指定します。 トレース ログには、トレース セッションの名前は、ログに保存されないために、traceview では、既定のセッションの名前を表示します。 この列を非表示にすることはできません。

<span id="State"></span><span id="state"></span><span id="STATE"></span>**状態**  
トレース セッションの状態を表示します。 この列の有効な値は、実行中、既存、停止、停止、グループ化、グループ化、および UNGROUPING です。

<span id="Event_Count"></span><span id="event_count"></span><span id="EVENT_COUNT"></span>**イベント数**  
リアルタイムのトレース セッションでは、この列には、セッション以降に受信した traceview で開始トレース メッセージの数が表示されます。 トレース ログには、この列には、ログにトレース メッセージの数が表示されます。

<span id="Lost_Events"></span><span id="lost_events"></span><span id="LOST_EVENTS"></span>**失われたイベント**  
セッションの開始後に失われたイベントの数が表示されます。 通常、イベントはトレース セッションが、バッファー内の領域を使い果たしたため、失われます。

<span id="Buffers_Read"></span><span id="buffers_read"></span><span id="BUFFERS_READ"></span>**バッファーの読み取り**  
Traceview で元のトレース メッセージを受信したバッファーの数を指定します。 既存のトレース ログには、この列には、トレース セッションで使用されていたバッファーの数が表示されます。

<span id="Flags"></span><span id="flags"></span><span id="FLAGS"></span>**フラグ**  
指定します、[トレース フラグ](trace-flags.md)トレース プロバイダー。 トレース フラグは、プロバイダーが生成されるトレース メッセージを決定します。 フラグの意味は、各プロバイダーによって個別に決定されます。

Traceview でを見つけることができる場合、[トレース メッセージのコントロール (.tmc) ファイル](trace-message-control-file.md)プロバイダーの選択フラグとレベルに表示される一覧から、**トレース フラグとレベル選択** ダイアログ ボックス。 このダイアログ ボックスを開くにはクリックして、**設定**の値、**フラグ**または**レベル**トレース セッション リスト内の列。

<span id="Flush_Time"></span><span id="flush_time"></span><span id="FLUSH_TIME"></span>**時間をフラッシュします**  
頻度を指定します (単位: 秒) (トレース ログまたは traceview でディスプレイに送信) トレース セッションのバッファーをフラッシュします。 既定値には 1 (秒) です。

これらのフラッシュを強制は、フラッシュ バッファーがいっぱいになったときと、トレース セッションを停止すると、自動的に行われるだけでなく発生します。 この列の 0 の値は、強制フラッシュが実行されないことを示します。

トレース セッションの実行中に、この値を変更することができます。

<span id="Max_Buf"></span><span id="max_buf"></span><span id="MAX_BUF"></span>**最大 Buf**  
トレース セッションで割り当てられるバッファーの最大数を指定します

既定値は、プロセッサ、物理メモリの量と使用のオペレーティング システムの数によって決まります。 トレース セッションの実行中に、この値を変更することができます。

<span id="Min_Buf"></span><span id="min_buf"></span><span id="MIN_BUF"></span>**Min Buf**  
トレース メッセージを格納するため最初に割り当てられるバッファーの数を指定します。

指定されている値に達するまで、多くのバッファーが割り当てられたバッファーがいっぱい、ときに、**最大 Buf**列。 既定値**Min Buf**はプロセッサ、物理メモリの量と使用のオペレーティング システムの数によって決まります。 トレース セッションの実行中に、この値を変更することはできません。

<span id="Buf_Size"></span><span id="buf_size"></span><span id="BUF_SIZE"></span>**バッファー サイズ**  
トレース セッションに割り当てられた各バッファーのサイズをキロバイト (KB) を指定します。 既定値は、プロセッサ、物理メモリの量と使用のオペレーティング システムの数によって決まります。 トレース セッションの実行中に、この値を変更することはできません。

<span id="Age"></span><span id="age"></span><span id="AGE"></span>**経過時間**  
(分単位) を使用していないトレース バッファーが保持される期間解放される前に指定します。 既定値は 15 分です。 この設定は、**減衰時間**のフィールド、[ログ セッションのパラメーター オプション](log-session-parameter-options.md) タブで、**ログ セッション オプションの高度な** ダイアログ ボックス。

この値は、Windows 2000 でのみ使用されます。 トレース セッションの実行中に、この値を変更することはできません。

<span id="Circular"></span><span id="circular"></span><span id="CIRCULAR"></span>**循環**  
トレース バッファーが循環することを指定し、各バッファーの最大サイズ (単位は MB) を指定します。

循環バッファーがいっぱいになった場合は、最も古いトレース メッセージを上書きする、バッファーの先頭に新しいトレース メッセージが書き込まれます。 既定では、トレース バッファーは、順次、循環できません。

トレース セッションの実行中に、この値を変更することはできません。

<span id="Sequential"></span><span id="sequential"></span><span id="SEQUENTIAL"></span>**シーケンシャル**  
トレース バッファーがシーケンシャルであることを指定し、各バッファーの最大サイズ (単位は MB) を指定します。

シーケンシャル バッファーがいっぱいになった場合、トレース メッセージは別のバッファーに書き込まれます。 または失われます。 既定では、トレース バッファーは、順次、循環しないられ、それぞれが 200 MB。

トレース セッションの実行中に、この値を変更することはできません。

<span id="New_File"></span><span id="new_file"></span><span id="NEW_FILE"></span>**新しいファイル**  
既存のログが、指定した値に達するたびに、新しいトレース ログ (.etl) を作成します。 値は、メガバイト (MB) 単位で、各ログ ファイルの最大サイズを指定します。 この設定は、**バッファー サイズ後にファイルを新しい開始**のフィールド、[ログ セッションのパラメーター オプション](log-session-parameter-options.md) タブで、**ログ セッション オプションの高度な** ダイアログ ボックス。

プロバイダーはときに生成するトレースのログは、選択した場合にのみ、この値は有効、[ログ トレース イベントのデータ ファイルのオプションを](basic-trace-session-options.md)上、**ログ セッション オプション**ページ。 このオプションは循環バッファーまたはログからの影響を与えません、[トレース セッションの NT Kernel Logger](nt-kernel-logger-trace-session.md)します。 Windows 2000 ではサポートされません。

<span id="Global_Seq"></span><span id="global_seq"></span><span id="GLOBAL_SEQ"></span>**グローバル シーケンス**  
各トレース メッセージのグローバル シーケンス番号を生成します。

グローバル シーケンス番号は、コンピューター上のすべてのトレース セッションに一意です。 既定値は**FALSE**します。

このパラメーターは、Windows 2000 ではサポートされていませんからのログに影響を与えません、[トレース セッションの NT Kernel Logger](nt-kernel-logger-trace-session.md)します。

<span id="Local_Seq"></span><span id="local_seq"></span><span id="LOCAL_SEQ"></span>**ローカル Seq**  
各トレース メッセージをローカルのシーケンス番号を生成します。 既定値は**TRUE**します。

ローカルのシーケンス番号は、トレース セッション内で一意です。

このパラメーターは、Windows 2000 ではサポートされていませんからのログに影響を与えません、[トレース セッションの NT Kernel Logger](nt-kernel-logger-trace-session.md)します。

<span id="Level"></span><span id="level"></span><span id="LEVEL"></span>**レベル**  
指定します、[トレース レベル](trace-level.md)トレース プロバイダー。 トレース レベルは、プロバイダーが生成されるトレース メッセージを決定します。 レベル値の意味は、各プロバイダーによって個別に決まります。 通常、詳細のレベルの増加を表します。

Traceview でを見つけることができる場合、[トレース メッセージのコントロール (.tmc) ファイル](trace-message-control-file.md)プロバイダーの選択フラグとレベルに表示される一覧から、**トレース フラグとレベル選択** ダイアログ ボックス。 このダイアログ ボックスを開くにはクリックして、**設定**の値、**フラグ**または**レベル**トレース セッションの一覧内の列。

トレース レベルの詳細については、の説明を参照して、 *EnableLevel*のパラメーター、 **EnableTrace** Microsoft Windows SDK のドキュメント内の関数。

<span id="WinDbg"></span><span id="windbg"></span><span id="WINDBG"></span>**WinDbg**  
リダイレクトは WinDbg、KD するメッセージをトレース traceview でウィンドウに表示する方法だけでなく、どちらが有効です。 このオプションは 3 KB、WinDbg で許可される最大サイズにも、バッファーのサイズを設定します。 表示される値、 **Buf サイズ**列は無視されます。

デバッガーでは、トレース メッセージを表示するに wmitrace.dll と traceprt.dll する必要がありますにホスト コンピューターで、デバッガーの検索パス。 また、トレースのトレース メッセージのメッセージ形式のファイルを検索するデバッガーを有効にする必要があります使用して、 **! wmitrace.searthpath**デバッガー拡張機能を特殊化または % のトレースの値を設定\_形式\_検索\_%path% 環境変数。 WinDbg と WMI のトレースの拡張機能については、Windows のツールのデバッグを参照してください。

<span id="Ignore_Traceview"></span><span id="ignore_traceview"></span><span id="IGNORE_TRACEVIEW"></span>**Traceview で無視します。**  
Traceview でアクションに関連するトレース メッセージを抑制します。

<span id="Max_Trace_Records"></span><span id="max_trace_records"></span><span id="MAX_TRACE_RECORDS"></span>**最大のトレース レコード**  
新しいメッセージを確保するために最も古いメッセージを上書きを開始する前に traceview で格納するトレース メッセージの最大数を示します。

値**0**最大値がないことと traceview ですべてを保持するメッセージをそれらが上書きされないことを意味します。 既定値は**65536**、ほとんどのシステムは、推奨される値。 大きな値には、重要な遅延を引き起こす可能性があります。

この設定は、**ファイル サイズの仮想**のフィールド、[ログ セッションのパラメーター オプション](log-session-parameter-options.md) タブで、**ログ セッション オプションの高度な** ダイアログ ボックス。

<span id="Log_File_Name"></span><span id="log_file_name"></span><span id="LOG_FILE_NAME"></span>**ログ ファイルの名前**  
イベント トレース ログ (.etl) ファイルの場所と名前が表示されます。 リアルタイムのトレース セッションでは、この列には、トレース メッセージが書き込まれるトレース ログの名前が表示されます。 既存のログ ファイル メッセージの読み取り元のトレース ログの名前が表示されます。

<span id="Save_As_Default"></span><span id="save_as_default"></span><span id="SAVE_AS_DEFAULT"></span>**既定値として保存します。**  
このオプションは、列名ではありません。 これは、将来のトレース セッションの既定値として現在表示されている列の構成を保存するコマンドです。 詳細についてを参照してください「、列の構成を保存しています」[トレース セッション リスト機能](trace-session-list-features.md)します。

 

 





