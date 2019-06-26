---
title: Tracelog のコマンド構文
description: トレース ログがコマンド (またはアクション) を開始、停止、およびトレース セッションを制御します。
ms.assetid: 13c85a1e-77ea-47d7-bb97-ff9141a8a531
keywords:
- Tracelog コマンド構文のドライバーの開発ツール
topic_type:
- apiref
api_name:
- Tracelog Command Syntax
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d71b143e2a15f8997fb29e3c8ae36cc19eac8e3e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353461"
---
# <a name="tracelog-command-syntax"></a>Tracelog のコマンド構文


トレース ログがコマンド (またはアクション) を開始、停止、および制御を[トレース セッション](trace-session.md)します。

> [!NOTE]
> トレース セッションを制御するには、Performance Log Users グループまたはコンピューターの Administrators グループのメンバーである (**管理者として実行**)。

```
    tracelog [actions] [options] | [-h | -help | -?] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター

トレース ログのパラメーターについては、次を参照してください\[ [*アクション*](#actions) \] \[ [*オプション*](#options)\]。

### <a name="actions"></a>\[*アクション*\]

<span id="_______-addautologger__LoggerName_"></span><span id="_______-addautologger__loggername_"></span><span id="_______-ADDAUTOLOGGER__LOGGERNAME_"></span> **-addautologger** \[*LoggerName*\]  
自動ロガーのセッションのレジストリ エントリを構成します。 自動ロガー、セッションは、システムの起動中にドライバーやその他のトレース プロバイダーのアクティビティをトレースするための推奨される方法です。 使用してセッション GUID を指定する必要があります、 **- sessionguid**オプション。 **Tracelog addautologger**コマンドでは、同じオプションとして、 **Tracelog-開始**コマンド。

<span id="_______-capturestate__LoggerName_"></span><span id="_______-capturestate__loggername_"></span><span id="_______-CAPTURESTATE__LOGGERNAME_"></span> **-capturestate** \[*LoggerName*\]  
要求を有効になっているすべてのプロバイダー*ロガー*状態情報を記録します。 有効になっているキーワードは、ログに記録される情報の種類を判断します。

<span id="_______-disable__LoggerName_"></span><span id="_______-disable__loggername_"></span><span id="_______-DISABLE__LOGGERNAME_"></span> **-disable** \[*LoggerName*\]  
指定されたトレース プロバイダーを無効にします。 プロバイダーが無効にするで継続して実行するが、トレース メッセージの生成を停止します。

**Tracelog-停止**コマンドは、セッションを停止する前に、トレース プロバイダーを無効にします。 トレース セッションを停止する前にプロバイダーを無効にする必要はありません。 ただし、使用することができます、**トレース ログに無効にする**トレース セッションを停止することがなく、選択したプロバイダーを無効にするコマンド。

トレース プロバイダーから、トレース セッション バッファーにトレース メッセージを送信を停止して無効にすると、バッファーをフラッシュしたり、トレース セッションを停止しません。 使用、 **tracelog-フラッシュ**コマンド バッファーをフラッシュして、 **tracelog-停止**または**tracelog-x**トレース セッションを停止 (stop すべて) コマンド。

トレース ログを使用して、 **EnableTrace**を実装する関数を**tracelog-を無効にする**コマンド。 この関数の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

<span id="_______-enable__LoggerName_"></span><span id="_______-enable__loggername_"></span><span id="_______-ENABLE__LOGGERNAME_"></span> **-有効にする** \[*ロガー*\]  
1 つまたは複数のトレース プロバイダーを有効、*ロガー*セッションをトレースします。

プロバイダーを有効にすると、プロバイダーはトレース メッセージを生成してトレース セッションのバッファーに送信します。 プロバイダーが実行されていない (またはが読み込まれていない) 有効にすると、システム*前レジスタ*プロバイダーは、ETW 登録情報データベース プロバイダーの領域を予約し、有効にするコマンドを保存します。 プロバイダーは起動して、実際は保存されている有効にするコマンドを受信し、セッションにトレース メッセージの送信を開始します。

**Tracelog-開始**コマンド、オプションで指定されたすべてのプロバイダーを使用する **- guid**パラメーター、 **tracelog-開始**コマンド。 個別に送信する必要はありません**tracelog-有効にする**コマンド。

使用することができます、 **tracelog-有効にする**コマンドを実行中のトレース セッションが、トレース中に、プロバイダーのフラグとレベルを変更するかを使用して無効になっているプロバイダーを再度有効にするプロバイダーを追加する、 **tracelog-を無効にします。** コマンド。

使用する場合、 **tracelog-を有効にする**コマンドでは、まず送信、 **tracelog-開始**トレース セッションを開始し、送信コマンド、 **tracelog-を有効にする**有効にするコマンドプロバイダー。

繰り返しが無効にしなくても、実行中のプロバイダーを有効にできます。 (これは、フラグとレベルを変更する。)

トレース フラグとで指定したトレース レベル、 **-フラグ**と **-レベル**によって表されるすべてのトレース プロバイダーに渡されるパラメーター、 **- guid**パラメーター。 各トレース プロバイダーのさまざまなフラグとレベルを指定するに、別の送信**tracelog-有効にする**コマンド プロバイダーごとに、独自のフラグとレベルの設定をします。

NT Kernel Logger フラグのいずれかを有効にしたかどうか (など **- noprocess**、 **- nothread**、 **- fio**、または **-cm**) グローバル ロガー トレース中にセッションが実行されて、グローバルのロガー セッションは、NT Kernel Logger のトレース セッションに変換されます。 この機能は、カーネル イベントをトレースするブート プロセス中に設計されています。

<span id="_______-enableex__LoggerName_"></span><span id="_______-enableex__loggername_"></span><span id="_______-ENABLEEX__LOGGERNAME_"></span> **-enableex** \[*LoggerName*\]  
同じ **-有効にする**します。 このオプションは、トレース ログの将来のバージョンで削除できます。

<span id="_______-enumguid______"></span><span id="_______-ENUMGUID______"></span> **-enumguid**   
システム上のプロバイダーを列挙します (または一覧表示します)[登録](registered-provider.md)を Event Tracing for Windows (ETW)。 Enumguid 表示については、次を参照してください。 [Tracelog Enumguid 表示](tracelog-enumguid-display.md)します。

トレース ログを使用して、 **EnumerateTraceGuids**を実装する関数を**tracelog enumguid**コマンド。 この関数の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

<span id="_______-enumguidex___guid_"></span><span id="_______-ENUMGUIDEX___GUID_"></span> **-enumguidex** \[ **\#** <em>guid</em>\]  
システム上のプロバイダーを列挙します (または一覧表示します)[登録](registered-provider.md)を Event Tracing for Windows (ETW)。 EnumguidEx 表示については、次を参照してください。 [Tracelog Enumguid 表示](tracelog-enumguid-display.md)します。

トレース ログを使用して、 **EnumerateTraceGuidsEx**を実装する関数を**tracelog enumguidex**コマンド。 この関数の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

<span id="_______-flush___LoggerName__"></span><span id="_______-flush___loggername__"></span><span id="_______-FLUSH___LOGGERNAME__"></span> **-フラッシュ** \[*ロガー*\]   
アクティブなバッファーのフラッシュ、*ロガー*セッションをトレースします。 場合*ロガー*が指定されていない、トレース ログのバッファーのフラッシュ、[トレース セッションの NT Kernel Logger](nt-kernel-logger-trace-session.md)します。

強制的な書き込みこれは、フラッシュとトレース メッセージのバッファーがいっぱいのときに、トレース セッションが停止したら、自動的に行われるだけでなく、フラッシュ フラッシュ タイマーによってアクティブ化されるだけでなく、( **-ft**)。

トレース セッションのバッファーをフラッシュするときに、バッファー内のイベントはすぐにトレース ログまたはトレース コンシューマーに配信されます。

フラッシュはトレース プロバイダーを無効にするまたはトレース メッセージをリダイレクトできません。 バッファーがフラッシュされると、トレース プロバイダーがバッファーにイベントを書き込んで続行されます。

トレース ログを使用して、 **FlushTrace**を実装する関数を**トレース ログのフラッシュ**コマンド。 この関数の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

使用することができます、 **tracelog-フラッシュ**コマンドを **-f** *Logfile*オプションを指定したバッファーにあるトレース メッセージをフラッシュする[トレース ログ](trace-log.md)(.etl) ファイル。 バッファー内のトレース セッションについてのみ、このパラメーターは有効です ( **-バッファリング**) は他のトレース セッションの種類、 **-f**パラメーターは無視されます。

このフラッシュは、バッファーの現在の内容のみに影響します。 将来のトレース メッセージはトレース ログにはリダイレクトしません。

<span id="_______-l______"></span><span id="_______-L______"></span> **-l** \[ *-lp*\]  
コンピューターで実行されているすべてのトレース セッションのプロパティを一覧表示します。

渡す場合、 **-lp**オプション、トレース ログはセッションごとに有効なプロバイダーをすべて一覧表示もできます。

<span id="_______-q___LoggerName_"></span><span id="_______-q___loggername_"></span><span id="_______-Q___LOGGERNAME_"></span> **-q** \[*LoggerName*\] \[ *-lp*\]  
(クエリ)、指定されたトレース セッションのプロパティを一覧表示します。 指定しない場合*ロガー*、トレース ログのクエリ、[トレース セッションの NT Kernel Logger](nt-kernel-logger-trace-session.md)します。

渡す場合、 **-lp**オプション、トレース ログは、セッションを有効になっているすべてのプロバイダー一覧表示もできます。

<span id="_______-remove_GlobalLogger______"></span><span id="_______-remove_globallogger______"></span><span id="_______-REMOVE_GLOBALLOGGER______"></span> **-remove GlobalLogger**   
削除し、グローバルのロガーのトレース セッションのレジストリ値を再初期化します。 開始エントリの値を 0 (起動しない) に設定し、その他のレジストリ エントリを削除します。 **Tracelog-削除**コマンドは、グローバル ロガー トレース セッションでのみ動作します。 その他のすべてのセッション名の値が無効です。

**Tracelog-削除**コマンドは必要ありません。 ただしの値を設定しない場合、**開始**システムを再起動するたびにエントリを 0 に、グローバル ロガー セッションの開始。

使用しない場合、 **tracelog-削除**コマンド、前回のセッション オプションはレジストリにも、送信する場合を除き、新しいセッションの使用は、 **tracelog-開始**コマンドを実行同じオプションに異なる値。

<span id="_______-start__LoggerName_"></span><span id="_______-start__loggername_"></span><span id="_______-START__LOGGERNAME_"></span> **-開始** \[*ロガー*\]  
使用してトレース セッションを開始、*ロガー*トレース セッションを表すことを選択します。

使用**GlobalLogger**として、*ロガー*を指定する、[ロガー トレース セッションのグローバル](global-logger-trace-session.md)します。 セッションは、コンピューターを再起動するときに起動します。

*ロガー*名前付けガイドラインについては、最大で 1,024 文字を任意の名前を Windows が満たしていることができます。 名前にスペースが含まれている場合は、名前を引用符で囲みます。 トレース ログは区別されません。

既定値は **"NT Kernel Logger"** します。 このパラメーターを省略すると場合、トレース ログが開始されます、[トレース セッションの NT Kernel Logger](nt-kernel-logger-trace-session.md)を使用する場合は、エラーを宣言し、 **- guid**異なるトレース プロバイダーを指定するパラメーター。

<span id="_______-stop__LoggerName_"></span><span id="_______-stop__loggername_"></span><span id="_______-STOP__LOGGERNAME_"></span> **-stop** \[*LoggerName*\]  
指定されたトレース セッションで、プロバイダーを無効にし、セッションを終了します。

**Tracelog-停止**コマンド両方トレース プロバイダーを無効にし、トレース セッションを停止します。 A **tracelog-を無効にする**コマンドには、トレース プロバイダーのみ無効にします。

起動する場合、[グローバル ロガーの起動時にセッション](boot-time-global-logger-session.md)コマンドを使用する必要がありますのカーネル イベントをトレースすると、**トレース ログの"NT Kernel Logger"を停止**または**tracelog-GlobalLoggerを停止**を停止します。 停止するコマンドのいずれかを使用すると、[グローバル ロガー トレース セッション](global-logger-trace-session.md)トレース セッションでは、トレース ログには、プロバイダーが停止しますが、レジストリ エントリの値はリセットされません。 グローバルのロガーのレジストリ エントリの値をリセットするには、使用**tracelog-削除**します。

<span id="-systemrundown__LoggerName_"></span><span id="-systemrundown__loggername_"></span><span id="-SYSTEMRUNDOWN__LOGGERNAME_"></span> **-systemrundown** \[*LoggerName*\]  
要求に向けられたランダウン イベントを記録する SystemTraceProvider*ロガー*セッション。 参照してください[構成し、SystemTraceProvider セッションを開始する](https://docs.microsoft.com/windows/desktop/ETW/configuring-and-starting-a-systemtraceprovider-session)については、トレース セッションを開始します。

このコマンドは、Windows 8 と Windows の以降のバージョンで使用できるだけです。

<span id="_______-timeout_______value______"></span><span id="_______-TIMEOUT_______VALUE______"></span> **-timeout** *値*   
プロバイダーを有効にするときに使用するミリ秒 (ms) で、タイムアウト値を指定します、 **tracelog-有効にする**コマンド。 既定のタイムアウトは、0 です。

タイムアウト値が 0 の場合、トレース ログは各プロバイダーの有効化のコールバックを呼び出すし、即座にコールバックが完了するを待たずに戻ります。

プロバイダーを同期的に有効にするには、タイムアウト値を指定します。 タイムアウト値を指定すると、トレース ログは各プロバイダーのコールバックが終了を有効にするか、タイムアウトが経過するまで待機します。

複数のプロバイダーを同時に有効にする場合、タイムアウトは順番に 1 つずつに適用されます。

<span id="_______-update_____LoggerName__"></span><span id="_______-update_____loggername__"></span><span id="_______-UPDATE_____LOGGERNAME__"></span> **-update** \[*LoggerName*\]   
**Tracelog-更新**コマンドは、実行中にトレース セッションのプロパティを変更します。

**Tracelog-更新**コマンド、-、**guid**パラメーターは、プライベートのトレース セッションを更新する場合のみ有効です ( **-um**)。を追加またはセッションの実行中に、標準のトレース セッションからプロバイダーを削除するには使用、 **tracelog-有効にする**と**tracelog-を無効にする**コマンド。

トレース ログ セッションを開始する場合 ( **-f**)、セッションをリアルタイムに更新することができます ( **-rt**)、引き続き、メッセージをトレース コンシューマーだけでなく、トレース ログに送信します。 更新することで、セッションからログを取り除くことはできません。 ただし、トレース ログ セッションをリアルタイムでのメッセージ配信を追加する前にする必要があります最初に使用する、**トレース ログのフラッシュ**コマンド バッファーをフラッシュします。

リアルタイムのセッションを開始する場合 ( **-rt**) し、トレース ログ セッションを更新 ( **-f**)、新しいトレース メッセージは、トレース コンシューマーに直接送信されなく; トレース ログにのみ送信されます。 トレース ログをリアルタイムのトレース セッションを追加するには、両方を使用 **-rt**と **-f**で、 **tracelog-更新**コマンド。 最初に使用する必要があるトレースのログ セッションをリアルタイムでのメッセージ配信を追加する前に、**トレース ログのフラッシュ**バッファーをフラッシュするコマンド。

更新することはできません、[グローバル ロガー トレース セッション](global-logger-trace-session.md)します。

プライベート (ユーザー モード) のセッションのトレース ログ ファイル名のみを更新することができます ( **-f**) とフラッシュ タイマー値 ( **-ft**)。

フラグとレベルを更新するには、使用、 **tracelog-有効にする**新しいフラグまたはレベルを使用してプロバイダーを再度有効にするコマンド。

トレース ログを使用して、 **ControlTrace**を実装する関数を**tracelog-更新**コマンド。 この関数の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

### <a name="options"></a>\[*オプション*\]

<span id="_-addtotriagedump_______"></span><span id="_-ADDTOTRIAGEDUMP_______"></span> **-addtotriagedump**   
> [!NOTE]
> このオプションは必要がありますが、デバッガーを使用してカーネル ダンプからイベントを表示する必要がある場合を除く使用されません。

アクティブなセッションのバッファーがトリアージ メモリ ダンプを追加できることを指定します。 トリアージ ダンプは、サイズに制限があり、バッファーを省略する場合、セッションのバッファーの最大サイズを超えたダンプ。

<span id="_______-append______"></span><span id="_______-APPEND______"></span> **-append**   
指定されたイベントのトレース ログ (.etl) ファイルにトレース メッセージを追加、 **-f**パラメーター。 既定では、新しいファイルを作成します。

このパラメーターを含むコマンドでのみ有効ですが **-f**を含めないでください **-rt**または **-cir**します。

<span id="_______-b_______BufferSize______"></span><span id="_______-b_______buffersize______"></span><span id="_______-B_______BUFFERSIZE______"></span> **-b** *BufferSize*   
サポート技術情報、トレース セッションに割り当てられた各バッファーのサイズを指定します。 既定値は、プロセッサ、物理メモリの量と使用のオペレーティング システムの数によって決まります。

<span id="-bt_n"></span><span id="-BT_N"></span> **-bt** *n*  
数を指定します (*n*) のバッファーにそれらのフラッシュを開始する前に入力します。 このオプションは、以降の Windows 8.1 で利用可能です。

<span id="_______-buffering______"></span><span id="_______-BUFFERING______"></span> **-buffering**   
バッファー内のトレース セッションを開始します。

バッファー内のトレース セッションでは、トレース メッセージはトレース バッファーに保持されます。 トレース コンシューマーに送信またはトレース ログに記録はありません。

<span id="_______-cir_______MaxFileSize______"></span><span id="_______-cir_______maxfilesize______"></span><span id="_______-CIR_______MAXFILESIZE______"></span> **-cir** *MaxFileSize*   
循環ログ (最も古いメッセージ経由で新しいメッセージをファイルの終わりのレコード) で、イベント トレース ログ (.etl) ファイルを指定します。 *MaxFileSize*ファイルの最大サイズを mb 単位で指定します。 なし、 *MaxFileSize*値、このパラメーターは無視されます。

既定値はシーケンシャル ファイルのサイズ制限なしでログに記録します。

<span id="_______-cm______"></span><span id="_______-CM______"></span> **-cm**   
レジストリ (構成マネージャー) へのアクセスの追跡を有効にします。 このパラメーターは、NT Kernel Logger のトレース セッションでのみ有効です。

<span id="_______-critsec______"></span><span id="_______-CRITSEC______"></span> **-critsec**   
プライベート トレース セッションでは、プロセスのクリティカル セクションのイベントをトレースします。 トレースのインストルメント化されていないものも含めて任意のユーザー モード プロセスに対して、クリティカル セクション プロセスのロガーを開始できます。

使用 **- pid**プロセスを指定します。 使用しない **- guid**で **- critsec**します。 システムでは、クリティカル セクションのトレースの場合は、カスタム GUID (CritSecGuid) を定義します。 使用することはできません **-ヒープ**と **- critsec**を同じコマンドでします。

<span id="_______-dpcisr______"></span><span id="_______-DPCISR______"></span> **-dpcisr**   
サービス要求 (Isr) イメージ読み込みイベントを中断する遅延プロシージャ呼び出し (Dpc) のトレースを有効 ( **- img**)、およびカーネル コンテキスト スイッチ。 このパラメーターは、NT Kernel Logger のトレース セッションでのみ有効です。

このオプションは、Windows Vista の Windows ドライバー キットおよび以降のバージョンの WDK に含まれるトレース ログのバージョンでのみサポートします。 **– Dpcisr**オプションでは使用できません、 **- eflag**オプション。

使用して、 **- UsePerfCounter**パラメーター **- dpcisr**します。 Tracerpt、書式設定し、DPC/ISR イベントを解釈するためのツールで、イベントごとに一意のタイムスタンプを提供する、このパラメーターが必要です。 解釈し、これらのイベントを書式設定については、以下の「コメント」を参照してください。

<span id="_______-eflag________n_________flag..._"></span><span id="_______-EFLAG________N_________FLAG..._"></span> **-eflag** *n* \[*flag*...\]  
追加のフラグを使用してカーネル イベントを有効に[トレース セッションの NT Kernel Logger](nt-kernel-logger-trace-session.md)、特に、DPC、ISR、およびコンテキストのトレースを有効にするフラグは、イベントを切り替えます。 **- Eflag**オプションでは使用できません、 **– dpcisr**オプション。

<span id="_______-enableproperty________n______"></span><span id="_______-ENABLEPROPERTY________N______"></span> **-enableproperty** *n*   
説明を参照して*EnabledProperties*で、 *EnableParameters*へのパラメーターとして渡された構造体[EnableTraceEx2](https://go.microsoft.com/fwlink/p/?linkid=155061)の説明、およびサポートされている値。

<span id="-EventIdFilter_____-in-out_n_id1_id2_..."></span><span id="-eventidfilter_____-in-out_n_id1_id2_..."></span><span id="-EVENTIDFILTER_____-IN-OUT_N_ID1_ID2_..."></span> **-EventIdFilter** { **-in**| **-out**} **** *n* **** *id1 id2 ...*  
イベント id フィルターを指定する*n*イベント id (許可される最大の 64 イベント id)。 このオプションは、以降の Windows 8.1 で利用可能です。

<span id="___-ExeFilter____Executable_file____Executable_file_...__"></span><span id="___-exefilter____executable_file____executable_file_...__"></span><span id="___-EXEFILTER____EXECUTABLE_FILE____EXECUTABLE_FILE_...__"></span> **-ExeFilter** *実行可能ファイル\_ファイル* \[ **;** *実行可能ファイル\_ファイル*.\]   
フィルター処理する実行可能ファイルの名前を指定します。 ファイルの一覧を指定することができます。 セミコロンを使用してファイル名を区切ります。 一覧にないファイルが除外されます。 このオプションは、以降の Windows 8.1 で利用可能です。

<span id="_______-f___LogFile_"></span><span id="_______-f___logfile_"></span><span id="_______-F___LOGFILE_"></span> **-f** \[*LogFile*\]  
トレースのログ セッションを開始します。 *ログ ファイル*イベント トレース ログ (.etl) ファイルのファイル名とパス (省略可能) を指定します。 既定値は c:\\LogFile.etl します。 リモート コンピューター上のファイルを配置するには、パスに、コンピューター名または IP アドレスが含まれます。

使用する場合 **-rt**で **-f**、コンシューマー、およびイベント トレース ログ ファイルにトレース メッセージが送信されます。 使用することはできません **-rt**または **-f**で **-バッファリング**します。

<span id="_______-fio______"></span><span id="_______-FIO______"></span> **-fio**   
ファイル I/O イベントの追跡を有効にします。 このパラメーターは、NT Kernel Logger のトレース セッションでのみ有効です。

<span id="_______-flag_______Flag______"></span><span id="_______-flag_______flag______"></span><span id="_______-FLAG_______FLAG______"></span> **-フラグ***フラグ*   
> [!NOTE]
> フラグがキーワードに置き換えられました。 使用 **- matchanykw** WPP プロバイダーを有効にする場合を除き、します。

指定します、[トレース フラグ](trace-flags.md)の[プロバイダー](trace-provider.md)トレース セッションでします。 フラグの値は、トレース プロバイダーが生成されるイベントを決定します。

*フラグ*10 進数または 16 進数形式で、トレース プロバイダーで定義されているフラグの値を表します。 既定値は 0 です。 0xFF000000 を通じて 0x01000000 からの値は、将来使用するために予約されています。

フラグの値の意味は、各トレース プロバイダーによって個別に定義されます。 通常、フラグは、しだいに詳細レポートのレベルを表します。

指定されたフラグ値、 **tracelog-開始**コマンドは、トレース セッションで、すべてのトレース プロバイダーに適用されます。 トレース プロバイダーごとにさまざまなフラグを設定するには、使用**tracelog-有効にする**します。

<span id="_______-ft_______FlushTime______"></span><span id="_______-ft_______flushtime______"></span><span id="_______-FT_______FLUSHTIME______"></span> **-ft** *FlushTime*   
どのくらいの頻度 (秒単位)、トレース メッセージ バッファーがフラッシュされるかを指定します。 フラッシュ時間の最小値は、1 秒です。 既定値は 0 (フラッシュを強制しないです)。

強制的な書き込みこれはトレース セッションを停止すると、トレース メッセージのバッファーがいっぱいのときに自動的に行われるフラッシュです。

参照してください、**トレース ログのフラッシュ コマンド**します。

<span id="_______-guid___GUID___GUIDFile_"></span><span id="_______-guid___guid___guidfile_"></span><span id="_______-GUID___GUID___GUIDFILE_"></span> **-guid** { *\#GUID* | *ファイル* |  *\*名前*}  
指定されたトレース プロバイダーを有効にします。

ファイルを指定すると場合、トレース ログは、ファイルに指定されたすべてのプロバイダーに、トレースを有効になります。 ファイルは、として書式設定する必要があります。

```text
; comment line
guid1;matchanykeyword;level
guid2;matchanykeyword;level
```

プロバイダーの GUID が指定されている場合、GUID が前に番号記号をする必要があります ( *\#* )。

プロバイダー名が指定されている場合、名前が前に、アスタリスクをする必要があります ( *\** )。 名前と同じアルゴリズムを使用して GUID に変換されます。NET のイベント ソース。 この GUID は、プロバイダーを有効に使用されます。

このパラメーターを省略すると、トレース プロバイダーがないメッセージを送信トレース セッション。 ただし、トレース セッションを開始した後は使用できます、 **tracelog-有効にする**セッションの 1 つまたは複数のトレース プロバイダーを有効にするコマンド。

<span id="_______-gs______"></span><span id="_______-GS______"></span> **-gs**   
各トレース メッセージのグローバル シーケンス番号を生成します。

グローバル シーケンス番号は、コンピューター上のすべてのトレース セッションに一意です。 既定では、シーケンス番号はありません。

このパラメーターは、NT Kernel Logger トレース セッションで有効ではありません。

<span id="_______-heap______"></span><span id="_______-HEAP______"></span> **-ヒープ**   
ユーザー モード プロセス ヒープ メモリのイベントをトレースします。 トレースのインストルメント化されていないものも含めて任意のユーザー モード プロセス ヒープ プロセスのロガーを開始できます。

使用 **- pid**プロセスを指定します。 使用しない **- guid**で **-ヒープ**します。 システムでは、ヒープ メモリのトレースの場合は、カスタム GUID (HeapGuid) を定義します。 使用することはできません **-ヒープ**と **- critsec**を同じコマンドでします。

<span id="_______-hf______"></span><span id="_______-HF______"></span> **-hf**   
ハード ページ フォールト (ディスク アクセスを解決する必要があるページ フォールト) の追跡を有効にします。 このパラメーターは、NT Kernel Logger のトレース セッションでのみ有効です。

<span id="-hybridshutdown_stoppersist"></span><span id="-HYBRIDSHUTDOWN_STOPPERSIST"></span> **-hybridshutdown** {**stop**|**persist**}  
ハイブリッド シャット ダウンのロガーの動作を制御します。 このオプションは、以降 Windows 8 で使用できます。

*停止*セッションは、システムは、ハイブリッドのシャット ダウンを実行するときに停止が発生します。
*永続化*システムのハイブリッドのシャット ダウンからもう一度起動した後も続行するセッションになります。

<span id="_______-img______"></span><span id="_______-IMG______"></span> **-img**   
イメージの読み込みイベントの追跡を有効にします。 このパラメーターは、NT Kernel Logger のトレース セッションでのみ有効です。

<span id="___-independent___"></span><span id="___-INDEPENDENT___"></span> **-独立しました。**   
> [!NOTE]
> すべてのトレース セッションでは、Independent モードを有効にする必要があります。

Independent モード、トレース セッションを有効にします。 Independent モードにより、他の非依存しないモード セッションを破棄イベントを収集するセッションです。 このオプションは、以降の Windows 8.1 で利用可能です。

<span id="_______-kb______"></span><span id="_______-KB______"></span> **-kb**   
ログ ファイルのサイズをキロバイト (KB) を使用します。 既定ではメガバイト (MB です)。

<span id="_______-kd______"></span><span id="_______-KD______"></span> **-kd**   
KD または Windbg、トレース メッセージをリダイレクトする方がアタッチされています。 このパラメーターもトレース バッファーのサイズをデバッガーの最大バッファー サイズは 3 KB に設定し、いずれかを無視します **-b**コマンドのパラメーター。

トレース ログを使用したコマンドを送信するときに、デバッガーを実行している必要があります **-kd**します。 それ以外の場合、トレース ログは、応答を停止します。

カーネル デバッガーにトレース メッセージを表示する方法の詳細については、コメントを参照してください。

**-Lbr** *EventName\[ **+** EventName+...\]:Filter\[ **,** Filter,...\]*  
カーネル イベントでは、LBR のトレースを構成します。

使用**eflag ヘルプ**カーネル イベントの一覧についてはします。

<span id="_______-level________n______"></span><span id="_______-LEVEL________N______"></span> **-レベル** *n*   
指定します、[トレース レベル](trace-level.md)トレース セッションでプロバイダー。 レベルは、トレース プロバイダーが生成されるイベントを決定します。

*レベル*レベルの 10 進数または 16 進数形式で値を表します。 既定値は 0 です。

レベル値の意味は、各トレース プロバイダーによって個別に定義されます。 通常、トレース レベルは、(情報、警告、またはエラー)、イベントの重大度を表します。

指定されたレベルの値を**tracelog-開始**コマンドは、トレース セッションで、すべてのトレース プロバイダーに適用されます。 トレース プロバイダーごとにさまざまなレベルを設定するには、使用**tracelog-有効にする**します。

<span id="_______-lowcapacity______"></span><span id="_______-LOWCAPACITY______"></span> **-lowcapacity**   
> [!NOTE]
> しない限り、このオプションは使用しないメモリ コストを削減するために必要です。 このオプションを使用すると、各イベントをログに時間がかかります。

複数のプロセッサで生成されたイベントを収集するために、一度に 1 つのバッファーを使用します。 このオプションは、イベントを選択します。\_トレース\_いいえ\_1 秒あたり\_プロセッサ\_バッファリング ログ モードです。 詳細については、Windows SDK を参照してください。

<span id="_______-ls______"></span><span id="_______-LS______"></span> **-ls**   
各トレース メッセージをローカルのシーケンス番号を生成します。

ローカルのシーケンス番号は、トレース セッション内で一意です。 既定では、シーケンス番号はありません。

このパラメーターは、NT Kernel Logger トレース セッションで有効ではありません。

<span id="_______-max_______NumberOfBuffers______"></span><span id="_______-max_______numberofbuffers______"></span><span id="_______-MAX_______NUMBEROFBUFFERS______"></span> **-max** *NumberOfBuffers*   
トレース セッションのトレース ログによって割り当てられるバッファーの最大数を指定します。 既定値は、プロセッサ、物理メモリの量と使用のオペレーティング システムの数によって決まります。

<span id="_______-matchallkw________n______"></span><span id="_______-MATCHALLKW________N______"></span> **-matchallkw** *n*   
指定します、 *MatchAllKeyWord*イベントのカテゴリを制限するビットマスク、プロバイダーの書き込みし、と組み合わせて使用、 **- matchanykw**オプション。

このビットマスクは省略可能です。 イベントのキーワードで指定した条件を満たしている場合は、**matchanykw**オプション、プロバイダーがイベントを書き込むだけこのマスクのビットのすべてが、イベントのキーワードに存在するかどうか。 場合、このマスクは使用されません **- matchanykw**は 0 です。

トレース ログには、値が渡された*n*で、 *MatchAllKeyWord*のパラメーター、 [EnableTraceEx2](https://go.microsoft.com/fwlink/p/?linkid=155061)関数呼び出し。 詳細については、Windows SDK を参照してください。

<span id="_______-matchanykw________n______"></span><span id="_______-MATCHANYKW________N______"></span> **-matchanykw** *n*   
指定します、 *MatchAnyKeyword*イベントのカテゴリを決定するビットマスク プロバイダーに書き込みます。

プロバイダーは、このマスクで設定されたビットのいずれかと一致、イベントのキーワードのビットのいずれかのかどうか、イベントを書き込みます。 トレース ログには、値が渡された*n*で、 *MatchAnyKeyWord*のパラメーター、 [EnableTraceEx2](https://go.microsoft.com/fwlink/p/?linkid=155061)関数呼び出し。 詳細については、Windows SDK を参照してください。

<span id="_______-min_______NumberOfBuffers______"></span><span id="_______-min_______numberofbuffers______"></span><span id="_______-MIN_______NUMBEROFBUFFERS______"></span> **最小** *NumberOfBuffers*   
トレース メッセージを格納するために最初に割り当てられたバッファーの数を指定します。 バッファーがいっぱい、最大値に達するまで、トレース ログはバッファーを割り当てます。 既定値は、プロセッサ、物理メモリの量と使用のオペレーティング システムの数によって決まります。

<span id="_______-newfile_______MaxFileSize______"></span><span id="_______-newfile_______maxfilesize______"></span><span id="_______-NEWFILE_______MAXFILESIZE______"></span> **-newfile** *MaxFileSize*   
既存のファイルに達するたびに、新しいイベント トレース ログ (.etl) ファイルを作成します*MaxFileSize*します。 *MaxFileSize*各ログ ファイルの最大サイズを mb 単位で指定します。 なし、 *MaxFileSize*値、このパラメーターは無視されます。

使用する場合 **- newfile**、使用することも必要があります、 **-f** *ログ ファイル*パラメーターと値の*LogFile*を含む名前にする必要があります、文字 **%d** decimal パターン - trace%d.etl などを指定します。 コマンドがエラーで失敗するそれ以外の場合、\_無効な\_名。 Windows では、新しいファイルを作成するたびにファイル名の 10 進値をインクリメントします。

このパラメーターは、事前割り当てに無効な ( **- prealloc**)、循環ログ記録 ( **-cir**)、NT Kernel Logger セッション、またはプライベートのトレース セッションのです。

<span id="_______-nodisk______"></span><span id="_______-NODISK______"></span> **-nodisk**   
物理ディスク I/O イベントの追跡を無効にします。 このパラメーターは、NT Kernel Logger のトレース セッションでのみ有効です。

<span id="_______-nonet______"></span><span id="_______-NONET______"></span> **-nonet**   
TCP/IP とユーザー データグラム プロトコル (UDP) のイベントの追跡を無効にします。 このパラメーターは、NT Kernel Logger のトレース セッションでのみ有効です。

<span id="_______-noprocess______"></span><span id="_______-NOPROCESS______"></span> **-noprocess**   
開始と各プロセスの終了のトレースを無効にします。 このパラメーターは、NT Kernel Logger のトレース セッションでのみ有効です。

<span id="_______-nothread______"></span><span id="_______-NOTHREAD______"></span> **-nothread**   
開始と各スレッドの終了のトレースを無効にします。 このパラメーターは、NT Kernel Logger のトレース セッションでのみ有効です。

<span id="_______-paged______"></span><span id="_______-PAGED______"></span> **-paged**   
トレースのメッセージ バッファーのページング可能なメモリを使用します。 既定では、イベントのトレースは、バッファーの非ページ メモリを使用します。

非ページ メモリを必要とするプロバイダーはページング可能なメモリを使用するセッションにイベントを記録できません。

<span id="_______-pids________PIDs_PID__PID..._"></span><span id="_______-pids________pids_pid__pid..._"></span><span id="_______-PIDS________PIDS_PID__PID..._"></span> **pid -**  *\#Pid PID* \[ *PID*.\]  
ユーザー モードを指定します。 プロセスのヒープ メモリまたはクリティカル セクションのトレース セッションが実行されます。 のみ有効です **-ヒープ**または **- critsec**します。

*\#Pid*このパラメーターで Id が表示されたプロセスの数を指定します。 *PID*プロセス識別子を表します。 このパラメーターでは、最大 10 個の Pid を指定できます。

プロバイダーが 1 つのプログラムが複数のプロセスを作成する場合など、複数のプロセスで実行すると、複数の Pid を一覧表示します。

<span id="___-PidFilter____n_pid1_pid2_..."></span><span id="___-pidfilter____n_pid1_pid2_..."></span><span id="___-PIDFILTER____N_PID1_PID2_..."></span> **-PidFilter** *n* *pid1 pid2 ...*  
Pid のフィルターを指定します*n* Pid (許可されている最大 8)。 このオプションは、以降の Windows 8.1 で利用可能です。

<span id="_______-pf______"></span><span id="_______-PF______"></span> **-pf**   
すべてのページ フォールトの追跡を有効にします。 このパラメーターは、NT Kernel Logger のトレース セッションでのみ有効です。

<span id="___________________-PkgIdFilter____Package_Full_Name____Package_Full_Name..._"></span><span id="___________________-pkgidfilter____package_full_name____package_full_name..._"></span><span id="___________________-PKGIDFILTER____PACKAGE_FULL_NAME____PACKAGE_FULL_NAME..._"></span> **-PkgIdFilter** *パッケージのフルネーム* \[  * *; * * * パッケージのフルネーム*.\]  
パッケージ ID のフィルターを指定します。 パッケージ ファイルの一覧を指定することができます。 セミコロンを使用してファイル名を区切ります。

<span id="___-PkgAppIdFilter_____PRAID____PRAID..._"></span><span id="___-pkgappidfilter_____praid____praid..._"></span><span id="___-PKGAPPIDFILTER_____PRAID____PRAID..._"></span> **-PkgAppIdFilter** *PRAID* \[* *;***PRAID*...\]  
アプリのパッケージ相対識別子 (PRAID) フィルターを指定します。 PRAID は、パッケージ内のアプリケーションの一意の識別子です。 1 つ以上指定できます*PRAID*します。 セミコロンを使用して Id を区切ります。 このオプションは、Windows 8.1 以降、UWP アプリで利用できます。

<span id="-Pmc_Ctrs_Events"></span><span id="-pmc_ctrs_events"></span><span id="-PMC_CTRS_EVENTS"></span> **-Pmc** *Ctr1、... Ctr2: 名 + 名前 +.*  
指定したカーネル イベントでは、パフォーマンス モニター カウンター (PMC) サンプリングを構成します。 このオプションは、以降 Windows 8 で使用できます。

使用**ProfileSource ヘルプ**カウンターの一覧についてはします。
使用**eflag ヘルプ**カーネル イベントの一覧についてはします。

<span id="_______-prealloc______"></span><span id="_______-PREALLOC______"></span> **-prealloc**   
セッションを開始する前に、.etl ファイルの領域を予約します。

このパラメーターが必要です **-seq**または **-cir**で*MaxFileSize*します。 無効な **- newfile**します。

<span id="-ProfileSource_src"></span><span id="-profilesource_src"></span><span id="-PROFILESOURCE_SRC"></span> **-ProfileSource** *src*  
使用するプロファイルのソースを構成します。 ソースの一覧について、コマンドを使用して**tracelog - ProfileSource ヘルプ**します。 このオプションは、以降 Windows 8 で使用できます。

このオプションは、Windows 8 と Windows の以降のバージョンで使用できるだけです。

<span id="_______-rt______"></span><span id="_______-RT______"></span> **-rt**   
リアルタイムのトレース セッションを開始します。 (トレース ログ セッション ( **-f**)、既定値です)。

使用する場合 **-rt**と **-f**、およびイベント トレース ログ ファイルにトレース コンシューマーにトレース メッセージが送信されます。 使用することはできません **-rt**または **-f**で **-バッファリング**します。 詳細については、次を参照してください。[トレース セッション](trace-session.md)します。

<span id="_______-secure______"></span><span id="_______-SECURE______"></span> **-secure**   
保護モードでトレースを有効にします。 このオプションは、イベントを選択します。\_トレース\_SECURE\_モードのログ モードです。 イベントをトレース ログでセッションにログオンできるユーザーを制限\_ログ\_イベントのアクセスを許可します。

<span id="_______-sessionguid______"></span><span id="_______-SESSIONGUID______"></span> **-sessionguid**   
自動ロガー セッション GUID レジストリ値を指定します。

<span id="-SetProfInt_n_src"></span><span id="-setprofint_n_src"></span><span id="-SETPROFINT_N_SRC"></span> **-SetProfInt** *n* **** *src*  
> [!IMPORTANT]
> プロファイリングの間隔を変更することは推奨されません。

プロファイリングの間隔を構成します (*n*) 指定されたソースの場所*n* 100 ナノ秒の単位で。 既定では 10000 (これは 1 ミリ秒に相当) です。 このオプションは、以降 Windows 8 で使用できます。

<span id="_______-seq_______MaxFileSize______"></span><span id="_______-seq_______maxfilesize______"></span><span id="_______-SEQ_______MAXFILESIZE______"></span> **-seq** *MaxFileSize*   
イベント トレース ログ (.etl) ファイルに (ファイルの終わりに、イベントの記録の停止) の連続したログ記録を指定します。 *MaxFileSize*ファイルの最大サイズを mb 単位で指定します。 なし、 *MaxFileSize*値、このパラメーターは無視されます。

シーケンシャルなログ記録は、既定では、ですが、このパラメーターを使用するには、ファイルの最大サイズを設定するかを使用して **- prealloc**します。 このパラメーターがない場合は、ファイル サイズの上限はありません。

<span id="_______-sourceguid________SourceGuid______"></span><span id="_______-sourceguid________sourceguid______"></span><span id="_______-SOURCEGUID________SOURCEGUID______"></span> **-sourceguid** *SourceGuid*   
として渡された GUID を指定します、 *SourceId*パラメーターを[EnableTraceEx](https://go.microsoft.com/fwlink/p/?linkid=103398)または[EnableTraceEx2](https://go.microsoft.com/fwlink/p/?linkid=155061)関数。 *SourceId*プロバイダーを有効になっているセッションを識別します。

**-stackwalk** \[*イベント*\]  
上の履歴の収集へのカーネル イベントを指定します。 使用**eflag ヘルプ**カーネル イベントの一覧についてはします。 このパラメーターは、NT Kernel Logger またはシステム ログ トレース セッションに対してのみ有効です。

<span id="________________-StackWalkFilter_-in-outnid1_id2_..."></span><span id="________________-stackwalkfilter_-in-outnid1_id2_..."></span><span id="________________-STACKWALKFILTER_-IN-OUTNID1_ID2_..."></span> **-StackWalkFilter** { **-in**| **-out**}*nid1 id2 ...*  
イベント ID フィルターを指定する*n*イベント Id (最大 64 イベント Id は許可されている)。 このオプションは、以降の Windows 8.1 で利用可能です。

<span id="-systemlogger"></span><span id="-SYSTEMLOGGER"></span> **-systemlogger**  
ロガーは、SystemTraceProvider イベントを受け取ることができます。 参照してください[構成し、SystemTraceProvider セッションを開始する](https://docs.microsoft.com/windows/desktop/ETW/configuring-and-starting-a-systemtraceprovider-session)します。 このオプションは、以降 Windows 8 で使用できます。

<span id="_______-um______"></span><span id="_______-UM______"></span> **-um**   
このパラメーターはプライベートのトレース セッションを必要プライベート トレース セッションを指定します。

<span id="_______-UseCPUCycle______"></span><span id="_______-usecpucycle______"></span><span id="_______-USECPUCYCLE______"></span> **-UseCPUCycle**   
(「CPU のティック数」とも呼ばれます) プロセッサ周波数を使用すると、各トレース メッセージの時間を測定します。

このタイマーは、最高の考えられる解決策を提供しますが、機密性の高いためエラーは、システムの電源管理対象コンピューターとマルチプロセッサ コンピューターで特に発生しやすくなります。 などの場合は、ARM プロセッサを搭載したコンピューターでこのタイマーを指定すると、順序のイベントで、可能性があります。 代わりに、 **- UsePerfCounter**高解像度のトレースをお勧めします。

**-UsePerfCounter**は既定のタイマーは、イベントのトレース。

<span id="_______-UsePerfCounter______"></span><span id="_______-useperfcounter______"></span><span id="_______-USEPERFCOUNTER______"></span> **-UsePerfCounter**   
レコード、高解像度のパフォーマンス カウンターのクロック値、各トレース メッセージの解像度の低いシステム時刻ではなく。

パフォーマンス カウンターのクロックは、約 100 ナノ秒単位でカウント、ために、各イベントの一意のタイムスタンプを提供します。

**-UsePerfCounter**は既定のタイマーは、イベントのトレース。

<span id="_______-UseSystemTime______"></span><span id="_______-usesystemtime______"></span><span id="_______-USESYSTEMTIME______"></span> **-UseSystemTime**   
高解像度のパフォーマンス カウンターのクロック時間、各トレース メッセージではなく、システム時刻を記録します。 システム タイマーには、(100 ナノ秒のパフォーマンス カウンターの時計と比較して)、10 ミリ秒の解像度があるために、複数のイベントはシステムの同時を持つことができます。

**-UsePerfCounter**は既定のタイマーは、イベントのトレース。

<span id="_______-_____help___-_______"></span><span id="_______-_____HELP___-_______"></span> **-? | help | -?**    
使用方法に関する情報を表示します。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

次のコメントは、いくつかのトレース ログ コマンドに適用されます。

### <a name="span-idsyntaxerrorsspanspan-idsyntaxerrorsspansyntax-errors"></a><span id="syntax_errors"></span><span id="SYNTAX_ERRORS"></span>構文エラー

トレース ログには、エラーなど、変更できない設定を更新しようとすると、不適切な構文のすべての組み合わせに対しては表示されません。 代わりに、コマンドの無効な部分は無視され、成功メッセージが表示されます。

### <a name="span-idsystemloggersspanspan-idsystemloggersspansystem-loggers"></a><span id="system_loggers"></span><span id="SYSTEM_LOGGERS"></span>システムのロガー

Windows は、その一部は正しく動作するための重要な多くの目的で、トレース セッションを使用します。 起動していないすべてのトレース セッションは停止されません。

### <a name="span-idenumguidspanspan-idenumguidspanenumguid"></a><span id="enumguid"></span><span id="ENUMGUID"></span>Enumguid

判断するかどうかを**tracelog-開始**または**tracelog-有効にする**コマンドが成功した、使用、 **tracelog enumguid**かを確認するかどうか、プロバイダー コマンド有効にし、使用して、 **tracelog l (リスト)** トレース セッションのプロパティを調べるコマンド。

### <a name="span-idrealtimeandlogsessionsspanspan-idrealtimeandlogsessionsspanreal-time-and-log-sessions"></a><span id="real_time_and_log_sessions"></span><span id="REAL_TIME_AND_LOG_SESSIONS"></span>リアルタイムおよびセッションのログ

トレース セッションには、リアルタイムのトレース セッションとトレースのログ セッションの両方を指定できます。 含める場合は、 **-rt** (リアルタイム) と **-f**システム送信バッファーの内容をログとトレース コンシューマーの両方を同じコマンドで (ログ セッション) パラメーター。 ただし、トレース ログ セッションをリアルタイムでのメッセージ配信を追加する前にバッファーする必要がありますフラッシュを使用して、**トレース ログのフラッシュ**コマンド。

リアルタイムのセッションを開始する場合 ( **-rt**) し、ログ セッションを更新 ( **-f**)、新しいトレース メッセージがログ ファイルにのみ送信されます。 リアルタイムのセッションにログ ファイルを追加するには、両方を使用 **-rt**と **-f**で、 **tracelog-更新**コマンド。

ログ セッションを開始する場合 ( **-f**)、セッションをリアルタイムに更新することができます ( **-rt**)、引き続き、メッセージをトレース コンシューマーだけでなく、ログに送信します。 更新することで、セッションからログを取り除くことはできません。

表示する、またはリアルタイム回限りのセッションからトレース メッセージを保存することができますもなど使用するトレース コンシューマー、 [Tracefmt](tracefmt.md)、または使用[traceview で](traceview.md)、(トレース ログ) のようなトレース コント ローラーとトレースの両方であります。コンシューマー。 Tracefmt を使用する場合を含めることを確認する、 **-rt** Tracefmt コマンドのパラメーター。

### <a name="span-idflagsandlevelsspanspan-idflagsandlevelsspanflags-and-levels"></a><span id="flags_and_levels"></span><span id="FLAGS_AND_LEVELS"></span>フラグとレベル

ほとんどのトレース プロバイダーでは、フラグまたはレベルが、特定の値に設定しない限り、すべてのトレース メッセージは生成されません。 プロバイダーは、どのようなトレースしているかを制御するのにフラグまたはレベルを使用します。 イベントのトレース ログ ファイルが空の場合は、フラグと、トレース プロバイダー内のレベルを確認します。

トレース メッセージが常に生成されることを確認するには、次の手順を完了します。

1.  設定、**フラグ**パラメーターを 0 xffffffff すべてのフラグ設定を有効にします。

2.  設定、**レベル**を 255 にすべてのレベルの設定を有効にするパラメーター。

### <a name="span-idtheeflagparameterspanspan-idtheeflagparameterspanthe--eflag-parameter"></a><span id="the__eflag_parameter"></span><span id="THE__EFLAG_PARAMETER"></span>-Eflag パラメーター

トレース ログが、 **- eflag** (拡張フラグ) パラメーターの追加のフラグを有効にするように設計された、[トレース セッションの NT Kernel Logger](nt-kernel-logger-trace-session.md)--、ISR、DPC のトレースを有効にするフラグで最も顕著なとコンテキスト スイッチ イベント。 **Tracelog-開始**コマンドが含まれています、 **- dpcisr**パラメーターの使用、 **- eflag**パラメーターが不要になったお勧めしません。

### <a name="span-idoutdatedparametersspanspan-idoutdatedparametersspanoutdated-parameters"></a><span id="outdated_parameters"></span><span id="OUTDATED_PARAMETERS"></span>古いパラメーター

以前のバージョンのトレース ログを**tracelog-開始**コマンドがサポートされている、 **-rt b**パラメーターの組み合わせ。 この組み合わせは置き換えられました、 **-バッファリング**パラメーターが無効になっています。

**-X**パラメーターは、すべてのトレース セッションを停止する可能性がシステムが不安定になるので、削除されました。

**- Disableex**パラメーターが削除されました。 使用 **-を無効にする**代わりにします。

### <a name="span-idntkernelloggerspanspan-idntkernelloggerspannt-kernel-logger"></a><span id="nt_kernel_logger"></span><span id="NT_KERNEL_LOGGER"></span>NT Kernel Logger

NT Kernel Logger でトレース セッションを開始するからセッション名を省略、 **tracelog-開始**コマンドを使用しないでください、 **- guid**プロバイダー GUID ファイルを指定するパラメーター。 **"NT Kernel Logger"** は既定のセッションの名前です。

セッション名を省略するかは場合 **"NT Kernel Logger"** 、システムが使用する場合でも、NT Kernel Logger のトレース セッションを起動、 **- guid**以外の GUID を指定するパラメーター **SystemTraceControlGUID**、NT Kernel Logger トレース セッションのコントロールの GUID。 別の GUID を指定する場合、システム エラーが返されます、(「システムのロガーを受け入れませんアプリケーション guid」)、NT Kernel Logger のトレース セッションがまだ起動します。

既定で Tracelog NT Kernel Logger トレース セッションを開始すると、プロセス、スレッド、物理ディスク I/O、トレースと TCP/IP のイベントが、パラメーターを使用するにはこれらのイベントのトレースを無効にして、その他のイベントのトレースを有効にします。

### <a name="span-iddpcisreventsspanspan-iddpcisreventsspandpcisr-events"></a><span id="dpc_isr_events"></span><span id="DPC_ISR_EVENTS"></span>DPC/ISR イベント

Tracerpt タイムスタンプとシステムのパフォーマンス カウンター クロック時間が必要ですが、ため、トレース ログを使用して、 **- UsePerfCounter**トレース セッションを開始するときにパラメーター。

DPC と ISR イベントは、特別なインストルメンテーションによって収集されるために表示されない、**有効トレース**コマンドを確認するトレース ログを表示するテーブルの行。

詳細については、次を参照してください。[例 15。/ISR DPC 時間の計測](example-15--measuring-dpc-isr-time.md)します。
