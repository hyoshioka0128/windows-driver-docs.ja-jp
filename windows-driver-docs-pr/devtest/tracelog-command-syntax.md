---
title: Tracelog のコマンド構文
description: Tracelog には、トレースセッションを開始、停止、および制御するコマンド (またはアクション) があります。
ms.assetid: 13c85a1e-77ea-47d7-bb97-ff9141a8a531
keywords:
- Tracelog コマンド構文ドライバー開発ツール
topic_type:
- apiref
api_name:
- Tracelog Command Syntax
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db03eb5ca3e147095703fba8ec432b61d1bcabd1
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769702"
---
# <a name="tracelog-command-syntax"></a>Tracelog のコマンド構文


Tracelog には、[トレースセッション](trace-session.md)を開始、停止、および制御するコマンド (またはアクション) があります。

> [!NOTE]
> トレースセッションを制御するには、コンピューターの Performance Log Users グループまたは Administrators グループのメンバーである必要があります (**管理者として実行**)。

```
    tracelog [actions] [options] | [-h | -help | -?] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメータ

Tracelog パラメーターの詳細については、「 \[ [*actions*](#actions) \] \[ [*options*](#options)」を参照してください \] 。

### <a name="actions"></a>\[*措置*\]

<span id="_______-addautologger__LoggerName_"></span><span id="_______-addautologger__loggername_"></span><span id="_______-ADDAUTOLOGGER__LOGGERNAME_"></span>**-addautologger ロガー** \[*LoggerName*\]  
自動ロガーセッションのレジストリエントリを構成します。 ロガーセッションは、システムの起動時に、ドライバーまたはその他のトレースプロバイダーのアクティビティをトレースするために推奨される方法です。 セッション GUID は、 **-sessionguid**オプションを使用して指定する必要があります。 **トレースログ-addautologger ロガー**コマンドは、**トレースログ start**コマンドと同じオプションを受け取ります。

<span id="_______-capturestate__LoggerName_"></span><span id="_______-capturestate__loggername_"></span><span id="_______-CAPTURESTATE__LOGGERNAME_"></span>**-capturestate** \[*LoggerName*\]  
すべてのプロバイダーに対して*LoggerName*を有効にし、状態情報をログに記録するよう要求します。 有効なキーワードは、ログに記録される情報の種類を決定するのに役立ちます。

<span id="_______-disable__LoggerName_"></span><span id="_______-disable__loggername_"></span><span id="_______-DISABLE__LOGGERNAME_"></span>**-disable** \[*LoggerName*\]  
指定されたトレースプロバイダーを無効にします。 プロバイダーを無効にすると、プロバイダーは引き続き実行されますが、トレースメッセージの生成を停止します。

**トレースログ stop**コマンドは、セッションを停止する前にトレースプロバイダーを無効にします。 トレースセッションを停止する前にプロバイダーを無効にする必要はありません。 ただし、トレースセッションを停止せずに、**トレースログ-disable**コマンドを使用して、選択したプロバイダーを無効にすることができます。

を無効にすると、トレースプロバイダーはトレースセッションバッファーへのトレースメッセージの送信を停止しますが、バッファーをフラッシュしたり、トレースセッションを停止したりすることはありません。 トレースセッションを停止するには、**トレースログ-flush**コマンドを使用してバッファーをフラッシュし、**トレースログ-stop**または**トレースログ-x** (すべて停止) コマンドを使用します。

トレースログは**enabletrace**関数を使用して**トレースログ-disable**コマンドを実装します。 この関数の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

<span id="_______-enable__LoggerName_"></span><span id="_______-enable__loggername_"></span><span id="_______-ENABLE__LOGGERNAME_"></span>**-enable** \[*LoggerName*\]  
*LoggerName*トレースセッションに対して1つ以上のトレースプロバイダーを有効にします。

プロバイダーを有効にすると、プロバイダーによってトレースメッセージが生成され、トレースセッションのバッファーに送信されます。 プロバイダーが実行されていない (または読み込まれていない) 場合は、プロバイダーを*事前登録*します。つまり、ETW 登録データベースにプロバイダーの領域を予約し、enable コマンドを保存します。 プロバイダーが起動し、実際に登録すると、保存された enable コマンドを受信し、セッションへのトレースメッセージの送信を開始します。

**トレースログ-** start コマンドを使用すると、**トレースログ-start**コマンドのオプションの**guid**パラメーターで指定されたプロバイダーを有効にすることができます。 個別の**トレースログ-enable**コマンドを送信する必要はありません。

**トレースログ enable**コマンドを使用すると、実行中のトレースセッションにプロバイダーを追加したり、トレース中にプロバイダーのフラグとレベルを変更したり、**トレースログ-disable**コマンドを使用して無効にしたプロバイダーを再度有効にしたりできます。

**トレースログ-enable**コマンドを使用する場合は、最初に**トレースログ-start**コマンドを送信してトレースセッションを開始し、**トレースログ-enable**コマンドを送信してプロバイダーを有効にします。

実行中のプロバイダーを無効にせずに、有効にすることができます。 (フラグとレベルを変更することもできます)。

**-フラグ**と**レベル**のパラメーターで指定するトレースフラグとトレースレベルは、 **-guid**パラメーターで表されるすべてのトレースプロバイダーに渡されます。 トレースプロバイダーごとに異なるフラグとレベルを指定するには、それぞれのフラグとレベルの設定を使用して、プロバイダーごとに個別の**トレースログ-enable**コマンドを送信します。

グローバルロガートレースセッションの実行中に NT カーネルロガーフラグ ( **-noprocess**、 **-noprocess**、 **-fio**、または **-cm**など) のいずれかを有効にすると、グローバル logger セッションが nt カーネルロガートレースセッションに変換されます。 この機能は、ブートプロセス中にカーネルイベントをトレースするように設計されています。

<span id="_______-enableex__LoggerName_"></span><span id="_______-enableex__loggername_"></span><span id="_______-ENABLEEX__LOGGERNAME_"></span>**-enableex** \[*LoggerName*\]  
**-Enable と**同じです。 このオプションは、将来のバージョンの Tracelog では削除される可能性があります。

<span id="_______-enumguid______"></span><span id="_______-ENUMGUID______"></span>**-enumguid**   
Windows イベントトレーシング (ETW) に[登録](registered-provider.md)されているシステム上のプロバイダーを列挙 (または一覧表示) します。 Enumguid 表示の説明については、「 [Tracelog Enumguid の表示](tracelog-enumguid-display.md)」を参照してください。

トレースログは、 **EnumerateTraceGuids**関数を使用して**トレースログ-enumguid**コマンドを実装します。 この関数の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

<span id="_______-enumguidex___guid_"></span><span id="_______-ENUMGUIDEX___GUID_"></span>**-enum番組 x** \[ **\#**<em>guid</em>\]  
Windows イベントトレーシング (ETW) に[登録](registered-provider.md)されているシステム上のプロバイダーを列挙 (または一覧表示) します。 Enumsee x ディスプレイの説明については、「 [Tracelog Enumguid の表示](tracelog-enumguid-display.md)」を参照してください。

トレースログは、 **EnumerateTraceGuidsEx**関数を使用して**トレースログ-enumguidex**コマンドを実装します。 この関数の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

<span id="_______-flush___LoggerName__"></span><span id="_______-flush___loggername__"></span><span id="_______-FLUSH___LOGGERNAME__"></span>**-flush** \[*LoggerName*\]   
*LoggerName*トレースセッションのアクティブなバッファーをフラッシュします。 *LoggerName*が指定されていない場合、Tracelog は[NT カーネルロガートレースセッション](nt-kernel-logger-trace-session.md)のバッファーをフラッシュします。

この強制フラッシュは、トレースメッセージバッファーがいっぱいになったときや、トレースセッションが停止したとき、およびフラッシュタイマー (**-ft**) によってアクティブ化されたフラッシュに加えて、自動的に発生するフラッシュに加えて行われます。

トレースセッションのバッファーをフラッシュすると、バッファー内のイベントはすぐにトレースログまたはトレースコンシューマーに配信されます。

フラッシュでは、トレースプロバイダーを無効にしたり、トレースメッセージをリダイレクトしたりすることはありません。 バッファーがフラッシュされると、トレースプロバイダーはバッファーへのイベントの書き込みを続行します。

トレースログは、 **flushtrace**関数を使用して**トレースログ-flush**コマンドを実装します。 この関数の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

**-F** *Logfile*オプションと共に**トレースログ flush**コマンドを使用して、現在バッファー内にあるトレースメッセージを、指定された[トレースログ](trace-log.md)(.etl) ファイルにフラッシュすることができます。 このパラメーターは、バッファーされたトレースセッション (**-バッファリング**) に対してのみ有効です。その他の種類のトレースセッションでは、 **-f**パラメーターは無視されます。

このフラッシュは、バッファーの現在の内容にのみ影響します。 今後のトレースメッセージはトレースログにはリダイレクトされません。

<span id="_______-l______"></span><span id="_______-L______"></span>**-l** \[*-lp*\]  
コンピューター上で実行されているすべてのトレースセッションのプロパティを一覧表示します。

**-Lp**オプションを指定すると、tracelog では、各セッションに対して有効になっているすべてのプロバイダーの一覧も表示されます。

<span id="_______-q___LoggerName_"></span><span id="_______-q___loggername_"></span><span id="_______-Q___LOGGERNAME_"></span>**-q** \[*LoggerName* \]\[ *-lp*\]  
指定されたトレースセッションのプロパティを一覧表示 (クエリ) します。 *LoggerName*を指定しない場合、Tracelog は[NT カーネルロガートレースセッション](nt-kernel-logger-trace-session.md)を照会します。

**-Lp**オプションを渡すと、tracelog は、セッションに対して有効になっているすべてのプロバイダーの一覧を表示します。

<span id="_______-remove_GlobalLogger______"></span><span id="_______-remove_globallogger______"></span><span id="_______-REMOVE_GLOBALLOGGER______"></span>**-GlobalLogger を削除**します   
グローバルロガートレースセッションのレジストリ値を削除して再初期化します。 開始エントリの値を 0 (開始しない) に設定し、その他のレジストリエントリを削除します。 **トレースログ-remove**コマンドは、グローバルロガートレースセッションに対してのみ機能します。 その他のすべてのセッション名の値は無効です。

**トレースログ-remove**コマンドは必要ありません。 ただし、 **Start**エントリの値を0に設定しなかった場合は、システムを再起動するたびにグローバル Logger セッションが開始されます。

**トレースログ-remove**コマンドを使用しない場合、前のセッションのオプションは引き続きレジストリ内にあり、同じオプションに対して異なる値を指定して**トレースログ start**コマンドを送信しない限り、新しいセッションで使用されます。

<span id="_______-start__LoggerName_"></span><span id="_______-start__loggername_"></span><span id="_______-START__LOGGERNAME_"></span>**-開始** \[*LoggerName*\]  
トレースセッションを表すために選択した*LoggerName*を使用して、トレースセッションを開始します。

[グローバルロガートレースセッション](global-logger-trace-session.md)を指定するには、 **Globallogger**を*LoggerName*として使用します。 コンピューターを再起動すると、セッションが開始されます。

*LoggerName*には、Windows の名前付けガイドライン (最大1024文字) を満たす任意の名前を指定できます。 名前にスペースが含まれている場合は、名前を引用符で囲みます。 Tracelog では、大文字と小文字は区別されません。

既定値は **"NT カーネルロガー"** です。 このパラメーターを省略した場合、Tracelog は[NT カーネルロガートレースセッション](nt-kernel-logger-trace-session.md)を開始し、 **-guid**パラメーターを使用して別のトレースプロバイダーを指定すると、エラーを宣言します。

<span id="_______-stop__LoggerName_"></span><span id="_______-stop__loggername_"></span><span id="_______-STOP__LOGGERNAME_"></span>**-停止** \[*LoggerName*\]  
指定されたトレースセッションのプロバイダーを無効にしてから、セッションを終了します。

**トレースログ-stop**コマンドは、トレースプロバイダーを無効にし、トレースセッションを停止します。 **トレースログ-disable**コマンドは、トレースプロバイダーのみを無効にします。

カーネルイベントをトレースする[ブート時のグローバル Logger セッション](boot-time-global-logger-session.md)を開始する場合は、コマンド**トレースログ-stop "NT kernel logger"** または**トレースログ stop globallogger**を使用して停止する必要があります。 いずれかのコマンドを使用して[グローバルロガートレースセッション](global-logger-trace-session.md)トレースセッションを停止すると、tracelog はプロバイダーを停止しますが、レジストリエントリの値はリセットされません。 グローバル Logger レジストリエントリの値をリセットするには、**トレースログ-remove**を使用します。

<span id="-systemrundown__LoggerName_"></span><span id="-systemrundown__loggername_"></span><span id="-SYSTEMRUNDOWN__LOGGERNAME_"></span>**-systemrundown ダウン** \[*LoggerName*\]  
*LoggerName*セッションで指示されたログランダウンイベントを SystemTraceProvider に要求します。 トレースセッションの開始の詳細については[、「SystemTraceProvider セッションの構成と開始](https://docs.microsoft.com/windows/desktop/ETW/configuring-and-starting-a-systemtraceprovider-session)」を参照してください。

このコマンドは、Windows 8 以降のバージョンの Windows でのみ使用できます。

<span id="_______-timeout_______value______"></span><span id="_______-TIMEOUT_______VALUE______"></span>**-タイムアウト***値*   
**トレースログ-enable**コマンドでプロバイダーを有効にするときに使用するタイムアウト値をミリ秒 (ms) 単位で指定します。 既定のタイムアウトは0です。

タイムアウト値が0の場合、Tracelog は、コールバックが完了するのを待たずに、各プロバイダーの有効化コールバックを呼び出し、すぐに制御を戻します。

プロバイダーを同期的に有効にするには、タイムアウト値を指定します。 タイムアウト値を指定すると、Tracelog は、各プロバイダーのコールバックが終了するか、タイムアウトが経過するまで待機します。

一度に複数のプロバイダーを有効にすると、タイムアウトは順番に1つずつ適用されます。

<span id="_______-update_____LoggerName__"></span><span id="_______-update_____loggername__"></span><span id="_______-UPDATE_____LOGGERNAME__"></span>**-更新** \[*LoggerName*\]   
**トレースログ-update**コマンドを実行すると、トレースセッションのプロパティが変更されます。

**トレースログ-update**コマンドでは、-**guid**パラメーターは、プライベートトレースセッション (**-um**) を更新する場合にのみ有効です。セッションの実行中に標準のトレースセッションのプロバイダーを追加または削除するには、**トレースログ-enable**および**トレースログ-disable**コマンドを使用します。

トレースログセッション (**-f**) を開始すると、リアルタイムセッション (**-rt**) に更新できますが、トレースコンシューマーに加えて、メッセージは引き続きトレースログに送信されます。 を更新することで、セッションからログを削除することはできません。 ただし、リアルタイムのメッセージ配信をトレースログセッションに追加する前に、まず**トレースログ-flush**コマンドを使用してバッファーをフラッシュする必要があります。

リアルタイムセッション (**-rt**) を開始してからトレースログセッション (**-f**) に更新すると、新しいトレースメッセージは直接トレースコンシューマーに送信されなくなります。これらはトレースログにのみ送信されます。 トレースログをリアルタイムのトレースセッションに追加するには、 **-rt**と **-f**の両方を**トレースログ-update**コマンドで使用します。 リアルタイムのメッセージ配信をトレースログセッションに追加する前に、まず**トレースログ-flush**コマンドを使用してバッファーをフラッシュする必要があります。

[グローバルロガートレースセッション](global-logger-trace-session.md)を更新することはできません。

プライベート (ユーザーモード) のトレースセッションでは、ログファイル名 (**-f**) とフラッシュタイマーの値 (**-ft**) のみを更新できます。

フラグとレベルを更新するには、**トレースログ-enable**コマンドを使用して、新しいフラグまたはレベルでプロバイダーを再び有効にします。

トレースログは、 **controltrace**関数を使用して**トレースログ-update**コマンドを実装します。 この関数の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

### <a name="options"></a>\[*オプション*\]

<span id="_-addtotriagedump_______"></span><span id="_-ADDTOTRIAGEDUMP_______"></span>**-addtotriagedump**   
> [!NOTE]
> デバッガーを使用してカーネルダンプからイベントを表示する必要がある場合を除き、このオプションは使用しないでください。

セッションのアクティブなバッファーをトリアージメモリダンプに追加できることを指定します。 トリアージダンプのサイズは制限されており、セッションのバッファーが原因でダンプが最大サイズを超えると、バッファーは残ります。

<span id="_______-append______"></span><span id="_______-APPEND______"></span>**-追加**   
**-F**パラメーターによって指定されたイベントトレースログ (.etl) ファイルにトレースメッセージを追加します。 既定では、新しいファイルが作成されます。

このパラメーターは、 **-f**を含むコマンドでのみ有効で、 **-rt**または **-cir**は含まれません。

<span id="_______-b_______BufferSize______"></span><span id="_______-b_______buffersize______"></span><span id="_______-B_______BUFFERSIZE______"></span>**-b** *BufferSize*   
トレースセッションに割り当てられた各バッファーのサイズを KB 単位で指定します。 既定値は、プロセッサの数、物理メモリの量、および使用されているオペレーティングシステムによって決まります。

<span id="-bt_n"></span><span id="-BT_N"></span>**-bt** *n*  
フラッシュを開始する前に、入力するバッファーの数 (*n*) を指定します。 このオプションは、Windows 8.1 から使用できます。

<span id="_______-buffering______"></span><span id="_______-BUFFERING______"></span>**-バッファリング**   
バッファーされたトレースセッションを開始します。

バッファーされたトレースセッションでは、トレースメッセージはトレースバッファーに保持されます。 トレースコンシューマーには送信されず、トレースログに記録されません。

<span id="_______-cir_______MaxFileSize______"></span><span id="_______-cir_______maxfilesize______"></span><span id="_______-CIR_______MAXFILESIZE______"></span>**-cir** *MaxFileSize*   
イベントトレースログ (.etl) ファイル内の循環ログ (ファイルの終わり、最も古いメッセージの新しいメッセージを記録します) を指定します。 *MaxFileSize*ファイルの最大サイズを MB 単位で指定します。 *MaxFileSize*値がない場合、このパラメーターは無視されます。

既定では、ファイルサイズの制限のない順次ログが使用されます。

<span id="_______-cm______"></span><span id="_______-CM______"></span>**-cm**   
レジストリ (Configuration Manager) アクセスのトレースを有効にします。 このパラメーターは、NT カーネルロガートレースセッションに対してのみ有効です。

<span id="_______-critsec______"></span><span id="_______-CRITSEC______"></span>**-critsec**   
プライベートトレースセッション内のプロセスのクリティカルセクションイベントをトレースします。 クリティカルセクションプロセスロガーは、トレース用にインストルメント化されていないものも含め、任意のユーザーモードプロセスで開始できます。

プロセスを指定するには **、-pid**を使用します。 - **Guid**を **-critsec**と共に使用しないでください。 システムは、重要なセクショントレース用にカスタム GUID (CritSecGuid) を定義します。 同じコマンドで **-heap**と **-critsec**を使用することはできません。

<span id="_______-dpcisr______"></span><span id="_______-DPCISR______"></span>**-dpcisr**   
遅延プロシージャ呼び出し (Dpc)、割り込みサービス要求 (Isr)、イメージ読み込みイベント (**-img**)、およびカーネル内のコンテキストスイッチのトレースを有効にします。 このパラメーターは、NT カーネルロガートレースセッションに対してのみ有効です。

このオプションは、windows Vista 以降のバージョンの WDK 用 Windows Driver Kit に含まれる Tracelog のバージョンでのみサポートされています。 **– Dpcisr**オプションは、 **-eflag**オプションと共に使用することはできません。

- **Useperfcounter**パラメーターと **-dpcisr**を使用します。 このパラメーターは、各イベントに対して一意のタイムスタンプを提供します。 Tracerpt は、DPC/ISR イベントの書式設定と解釈に使用されるツールです。 これらのイベントの解釈と書式設定の詳細については、以下の「コメント」を参照してください。

<span id="_______-eflag________n_________flag..._"></span><span id="_______-EFLAG________N_________FLAG..._"></span>**-eflag** *n* \[ *フラグ*...\]  
[NT カーネルロガートレースセッション](nt-kernel-logger-trace-session.md)に追加のフラグ (特に、DPC、ISR、およびコンテキスト切り替えイベントのトレースを有効にするフラグ) を使用して、カーネルイベントを有効にします。 **-Eflag**オプションは、 **– dpcisr**オプションと共に使用することはできません。

<span id="_______-enableproperty________n______"></span><span id="_______-ENABLEPROPERTY________N______"></span>**-enableproperty** *n*   
説明とサポートされている値については、 [EnableTraceEx2](https://docs.microsoft.com/windows/win32/api/evntrace/nf-evntrace-enabletraceex2)にパラメーターとして渡される*enableparameters*構造体の*enabledproperties*の説明を参照してください。

<span id="-EventIdFilter_____-in-out_n_id1_id2_..."></span><span id="-eventidfilter_____-in-out_n_id1_id2_..."></span><span id="-EVENTIDFILTER_____-IN-OUT_N_ID1_ID2_..."></span>**-EventIdFilter** {**-** | **out**} * * * * *n*  ****  *id1 id2...*  
イベント id フィルターに*n 個*のイベント id (許容最大64イベント id) を指定します。 このオプションは、Windows 8.1 から使用できます。

<span id="___-ExeFilter____Executable_file____Executable_file_...__"></span><span id="___-exefilter____executable_file____executable_file_...__"></span><span id="___-EXEFILTER____EXECUTABLE_FILE____EXECUTABLE_FILE_...__"></span>**-Exefilter** *実行可能 \_ ファイル* \[ **;** *実行可能 \_ ファイル*...\]   
フィルター処理する実行可能ファイルの名前を指定します。 ファイルの一覧を指定できます。 ファイル名はセミコロンで区切ります。 一覧にないファイルは除外されます。 このオプションは、Windows 8.1 から使用できます。

<span id="_______-f___LogFile_"></span><span id="_______-f___logfile_"></span><span id="_______-F___LOGFILE_"></span>**-f** \[*ログファイル*\]  
トレースログセッションを開始します。 *LogFile*は、イベントトレースログ (.etl) ファイルのパス (省略可能) とファイル名を指定します。 既定値は C: \\ LogFile です。 ファイルをリモートコンピューターに配置するには、コンピューター名または IP アドレスをパスに含めます。

- **Rt**を **-f**と共に使用すると、トレースメッセージがコンシューマーおよびイベントトレースログファイルに送信されます。 - **Rt**または- **f**を **-バッファリング**と共に使用することはできません。

<span id="_______-fio______"></span><span id="_______-FIO______"></span>**-fio**   
ファイル i/o イベントのトレースを有効にします。 このパラメーターは、NT カーネルロガートレースセッションに対してのみ有効です。

<span id="_______-flag_______Flag______"></span><span id="_______-flag_______flag______"></span><span id="_______-FLAG_______FLAG______"></span>**-フラグ***フラグ*   
> [!NOTE]
> フラグはキーワードで置き換えられました。 WPP プロバイダーを有効にしない場合は **、-matchanykw**を使用します。

トレースセッションの[プロバイダー](trace-provider.md)の[トレースフラグ](trace-flags.md)を指定します。 フラグの値によって、トレースプロバイダーが生成するイベントが決まります。

*フラグ*は、トレースプロバイダーで定義された、10進数または16進数形式のフラグ値を表します。 既定値は 0 です。 0x01000000 から0xFF000000 までの値は、将来使用するために予約されています。

フラグ値の意味は、各トレースプロバイダーによって個別に定義されます。 通常、フラグは、より詳細なレポートレベルを表します。

**トレースログ start**コマンドで指定されたフラグ値は、トレースセッションのすべてのトレースプロバイダーに適用されます。 トレースプロバイダーごとに異なるフラグを設定するには、**トレースログ-enable**を使用します。

<span id="_______-ft_______FlushTime______"></span><span id="_______-ft_______flushtime______"></span><span id="_______-FT_______FLUSHTIME______"></span>**-ft** *flushtime*   
トレースメッセージバッファーをフラッシュする頻度を秒単位で指定します。 最小フラッシュ時間は1秒です。 既定値は 0 (強制フラッシュなし) です。

この強制フラッシュは、トレースメッセージバッファーがいっぱいになったときや、トレースセッションが停止したときに自動的に発生するフラッシュに加えて行われます。

**トレースログ-flush コマンド**を参照してください。

<span id="_______-guid___GUID___GUIDFile_"></span><span id="_______-guid___guid___guidfile_"></span><span id="_______-GUID___GUID___GUIDFILE_"></span>**-guid** {* \# guid*  |  *ファイル*  |  * \* 名*}  
指定されたトレースプロバイダーを有効にします。

ファイルが指定されている場合、Tracelog は、ファイルで指定されているすべてのプロバイダーのトレースを有効にします。 ファイルは次の形式で指定する必要があります。

```text
; comment line
guid1;matchanykeyword;level
guid2;matchanykeyword;level
```

プロバイダー GUID を指定する場合は、GUID をシャープ記号 () で続けるする必要があり *\#* ます。

プロバイダー名を指定する場合は、名前をアスタリスク () で続けるする必要があり *\** ます。 名前は、と同じアルゴリズムを使用して GUID に変換されます。NET のイベントソース。 この GUID は、プロバイダーを有効にするために使用されます。

このパラメーターを省略すると、トレースプロバイダーはトレースセッションにメッセージを送信しません。 ただし、トレースセッションを開始した後は、**トレースログ-enable**コマンドを使用して、そのセッションに対して1つ以上のトレースプロバイダーを有効にすることができます。

<span id="_______-gs______"></span><span id="_______-GS______"></span>**-gs**   
各トレースメッセージのグローバルシーケンス番号を生成します。

グローバルシーケンス番号は、コンピューター上のすべてのトレースセッションに対して一意です。 既定では、シーケンス番号はありません。

このパラメーターは、NT カーネルロガートレースセッションでは無効です。

<span id="_______-heap______"></span><span id="_______-HEAP______"></span>**-ヒープ**   
ユーザーモードプロセスのヒープメモリイベントをトレースします。 ヒーププロセスロガーは、トレース用にインストルメント化されていないものも含め、任意のユーザーモードプロセスで開始できます。

プロセスを指定するには **、-pid**を使用します。 **-Guid**を **-heap**と一緒に使用しないでください。 システムは、ヒープメモリトレース用のカスタム GUID (HeapGuid) を定義します。 同じコマンドで **-heap**と **-critsec**を使用することはできません。

<span id="_______-hf______"></span><span id="_______-HF______"></span>**-hf**   
ハードページフォールト (解決するためにディスクアクセスを必要とするページフォールト) のトレースを有効にします。 このパラメーターは、NT カーネルロガートレースセッションに対してのみ有効です。

<span id="-hybridshutdown_stoppersist"></span><span id="-HYBRIDSHUTDOWN_STOPPERSIST"></span>**-hybridshutdown** {**stop** | **persist**}  
ハイブリッドシャットダウン logger の動作を制御します。 このオプションは、Windows 8 以降で使用できます。

*停止*すると、システムがハイブリッドシャットダウンを実行したときにセッションが停止します。
*保持*すると、ハイブリッドシャットダウンから再びシステムが起動した後、セッションは続行されます。

<span id="_______-img______"></span><span id="_______-IMG______"></span>**-img**   
イメージ読み込みイベントのトレースを有効にします。 このパラメーターは、NT カーネルロガートレースセッションに対してのみ有効です。

<span id="___-independent___"></span><span id="___-INDEPENDENT___"></span>**-非依存**   
> [!NOTE]
> すべてのトレースセッションで独立モードを有効にする必要があります。

トレースセッションで独立モードを有効にします。 独立モードでは、セッションは、他の非依存モードのセッションによって削除されたイベントを収集できます。 このオプションは、Windows 8.1 から使用できます。

<span id="_______-kb______"></span><span id="_______-KB______"></span>**-kb**   
ログファイルのサイズにはキロバイト (KB) を使用します。 既定値はメガバイト (MB) です。

<span id="_______-kd______"></span><span id="_______-KD______"></span>**-kd**   
は、添付されているいずれかの方法で、KD または Windbg にトレースメッセージをリダイレクトします。 また、このパラメーターは、トレースバッファーのサイズを、デバッガーの最大バッファーサイズである 3 KB に設定し、コマンド内の **-b**パラメーターを無視します。

**-Kd**で tracelog コマンドを送信するときに、デバッガーが実行されている必要があります。 それ以外の場合、Tracelog は応答を停止します。

カーネルデバッガーでのトレースメッセージの表示の詳細については、「コメント」を参照してください。

**-Lbr** *eventname \[ **+** eventname +... \] : フィルター \[ **、** フィルター,... \] *  
カーネルイベントに対して LBR トレースを構成します。

カーネルイベントの一覧を表示するには **、-Eflag Help**を使用します。

<span id="_______-level________n______"></span><span id="_______-LEVEL________N______"></span>**-レベル** *n*   
トレースセッションのプロバイダーの[トレースレベル](trace-level.md)を指定します。 レベルによって、トレースプロバイダーが生成するイベントが決まります。

*Level*は、10進形式または16進数形式のレベル値を表します。 既定値は 0 です。

レベル値の意味は、各トレースプロバイダーによって個別に定義されます。 通常、トレースレベルは、イベントの重大度 (情報、警告、またはエラー) を表します。

**トレースログ start**コマンドで指定されたレベルの値は、トレースセッションのすべてのトレースプロバイダーに適用されます。 トレースプロバイダーごとに異なるレベルを設定するには、**トレースログ-enable**を使用します。

<span id="_______-lowcapacity______"></span><span id="_______-LOWCAPACITY______"></span>**-低容量**   
> [!NOTE]
> メモリコストを削減するために必要な場合を除き、このオプションは使用しないでください。 このオプションを使用すると、各イベントがログに出力される速度が低下します。

は、一度に1つのバッファーを使用して、複数のプロセッサで生成されたイベントを収集します。 このオプションでは、[ \_ プロセッサごとのイベントトレースなし] ログモードを選択し \_ \_ \_ \_ ます。 詳細については、Windows SDK を参照してください。

<span id="_______-ls______"></span><span id="_______-LS______"></span>**-ls**   
各トレースメッセージのローカルシーケンス番号を生成します。

ローカルシーケンス番号は、トレースセッション内で一意です。 既定では、シーケンス番号はありません。

このパラメーターは、NT カーネルロガートレースセッションでは無効です。

<span id="_______-max_______NumberOfBuffers______"></span><span id="_______-max_______numberofbuffers______"></span><span id="_______-MAX_______NUMBEROFBUFFERS______"></span>**-最大** *numberofbuffers*   
トレースセッションに対して Tracelog によって割り当てられるバッファーの最大数を指定します。 既定値は、プロセッサの数、物理メモリの量、および使用されているオペレーティングシステムによって決まります。

<span id="_______-matchallkw________n______"></span><span id="_______-MATCHALLKW________N______"></span>**-matchallkw** *n*   
プロバイダーが書き込むイベントのカテゴリを制限し、 **-matchanykw**オプションと共に使用する、 *MatchAllKeyWord*ビットマスクを指定します。

このビットマスクは省略可能です。 イベントのキーワードが-**matchanykw**オプションで指定された条件を満たしている場合、このマスク内のすべてのビットがイベントのキーワードに存在する場合にのみ、プロバイダーによってイベントが書き込まれます。 **-Matchanykw**が0の場合、このマスクは使用されません。

Tracelog は、 [EnableTraceEx2](https://docs.microsoft.com/windows/win32/api/evntrace/nf-evntrace-enabletraceex2)関数呼び出しの*MatchAllKeyWord*パラメーターに値*n*を渡します。 詳細については、Windows SDK を参照してください。

<span id="_______-matchanykw________n______"></span><span id="_______-MATCHANYKW________N______"></span>**-matchanykw** *n*   
プロバイダーが書き込むイベントのカテゴリを決定する*MatchAnyKeyword*ビットマスクを指定します。

イベントのいずれかのキーワードビットが、このマスクで設定されているいずれかのビットと一致する場合、プロバイダーはイベントを書き込みます。 Tracelog は、 [EnableTraceEx2](https://docs.microsoft.com/windows/win32/api/evntrace/nf-evntrace-enabletraceex2)関数呼び出しの*MatchAnyKeyWord*パラメーターに値*n*を渡します。 詳細については、Windows SDK を参照してください。

<span id="_______-min_______NumberOfBuffers______"></span><span id="_______-min_______numberofbuffers______"></span><span id="_______-MIN_______NUMBEROFBUFFERS______"></span>**-最小** *numberofbuffers*   
トレースメッセージを格納するために最初に割り当てられたバッファーの数を指定します。 バッファーがいっぱいになると、Tracelog は、最大値に達するまでより多くのバッファーを割り当てます。 既定値は、プロセッサの数、物理メモリの量、および使用されているオペレーティングシステムによって決まります。

<span id="_______-newfile_______MaxFileSize______"></span><span id="_______-newfile_______maxfilesize______"></span><span id="_______-NEWFILE_______MAXFILESIZE______"></span>**-newfile** *MaxFileSize*   
既存のファイルが*MaxFileSize*に到達するたびに、新しいイベントトレースログ (.etl) ファイルを作成します。 *MaxFileSize*各ログファイルの最大サイズを MB 単位で指定します。 *MaxFileSize*値がない場合、このパラメーターは無視されます。

**-Newfile**を使用する場合は、 **-f** *logfile*パラメーターも使用する必要があります。 *logfile*の値は、10進パターンを示す文字 **% d**を含む名前にする必要があります (例: トレース% d. .etl)。 それ以外の場合、コマンドは失敗し、 \_ 無効な名前が付けら \_ れます。 Windows は、新しいファイルを作成するたびに、ファイル名の10進値をインクリメントします。

このパラメーターは、事前割り当て (**-prealloc**)、循環ログ (**-CIR**)、NT カーネルロガーセッション、またはプライベートトレースセッションでは無効です。

<span id="_______-nodisk______"></span><span id="_______-NODISK______"></span>**-nodisk**   
物理ディスク i/o イベントのトレースを無効にします。 このパラメーターは、NT カーネルロガートレースセッションに対してのみ有効です。

<span id="_______-nonet______"></span><span id="_______-NONET______"></span>**-nonet**   
TCP/IP およびユーザーデータグラムプロトコル (UDP) イベントのトレースを無効にします。 このパラメーターは、NT カーネルロガートレースセッションに対してのみ有効です。

<span id="_______-noprocess______"></span><span id="_______-NOPROCESS______"></span>**-noprocess**   
各プロセスの開始と終了のトレースを無効にします。 このパラメーターは、NT カーネルロガートレースセッションに対してのみ有効です。

<span id="_______-nothread______"></span><span id="_______-NOTHREAD______"></span>**-nothread**   
各スレッドの開始と終了のトレースを無効にします。 このパラメーターは、NT カーネルロガートレースセッションに対してのみ有効です。

<span id="_______-paged______"></span><span id="_______-PAGED______"></span>**-ページ**   
は、ページング可能なメモリをトレースメッセージバッファーに使用します。 既定では、イベントトレースはバッファーに非ページングメモリを使用します。

非ページングメモリを必要とするプロバイダーは、ページング可能なメモリを使用するセッションにイベントを記録することはできません。

<span id="_______-pids________PIDs_PID__PID..._"></span><span id="_______-pids________pids_pid__pid..._"></span><span id="_______-PIDS________PIDS_PID__PID..._"></span>**-** pid pid * \# pid* \[ *pid*...\]  
ヒープメモリまたはクリティカルセクションのトレースセッションを実行するユーザーモードプロセスを指定します。 **-Heap**または **-critsec**でのみ有効です。

* \# Pid*このパラメーターに一覧表示されているプロセス id の数を指定します。 *PID*はプロセス識別子を表します。 このパラメーターでは、最大10個の Pid を指定できます。

1つのプログラムが複数のプロセスを作成する場合など、複数のプロセスでプロバイダーを実行する場合は、複数の Pid を一覧表示します。

<span id="___-PidFilter____n_pid1_pid2_..."></span><span id="___-pidfilter____n_pid1_pid2_..."></span><span id="___-PIDFILTER____N_PID1_PID2_..."></span>**-PidFilter** *n* *pid1 pid2...*  
*N* pid (最大8個の許容) を持つ Pid フィルターを指定します。 このオプションは、Windows 8.1 から使用できます。

<span id="_______-pf______"></span><span id="_______-PF______"></span>**-pf**   
すべてのページフォールトのトレースを有効にします。 このパラメーターは、NT カーネルロガートレースセッションに対してのみ有効です。

<span id="___________________-PkgIdFilter____Package_Full_Name____Package_Full_Name..._"></span><span id="___________________-pkgidfilter____package_full_name____package_full_name..._"></span><span id="___________________-PKGIDFILTER____PACKAGE_FULL_NAME____PACKAGE_FULL_NAME..._"></span>**-PkgIdFilter** *パッケージの完全名* \[  * *; * * * パッケージの完全な名前*...\]  
パッケージ ID フィルターを指定します。 パッケージファイルの一覧を指定できます。 ファイル名はセミコロンで区切ります。

<span id="___-PkgAppIdFilter_____PRAID____PRAID..._"></span><span id="___-pkgappidfilter_____praid____praid..._"></span><span id="___-PKGAPPIDFILTER_____PRAID____PRAID..._"></span>**-PkgAppIdFilter** *praid* \[ * *; * * * praid*...\]  
パッケージ相対アプリ識別子 (PRAID) フィルターを指定します。 PRAID は、パッケージ内のアプリケーションの一意の識別子です。 複数の*Praid*を指定できます。 Id はセミコロンで区切ります。 このオプションは、Windows 8.1 以降の UWP アプリで使用できます。

<span id="-Pmc_Ctrs_Events"></span><span id="-pmc_ctrs_events"></span><span id="-PMC_CTRS_EVENTS"></span>**-Pmc** *Ctr1、Ctr2,...: name + name +...*  
指定されたカーネルイベントに対して performance monitor counter (PMC) サンプリングを構成します。 このオプションは、Windows 8 以降で使用できます。

カウンターの一覧を表示するには **、-profilesource ヘルプ**を使用します。
カーネルイベントの一覧を表示するには **、-Eflag Help**を使用します。

<span id="_______-prealloc______"></span><span id="_______-PREALLOC______"></span>**-prealloc**   
セッションを開始する前に、.etl ファイルの領域を予約します。

このパラメーターには **、-seq**または **-cir**と*MaxFileSize*が必要です。 **-Newfile**では無効です。

<span id="-ProfileSource_src"></span><span id="-profilesource_src"></span><span id="-PROFILESOURCE_SRC"></span>**-Profilesource** *src*  
使用するプロファイルソースを構成します。 ソースの一覧を表示するには、コマンド**トレースログ-profilesource Help**を使用します。 このオプションは、Windows 8 以降で使用できます。

このオプションは、Windows 8 以降のバージョンの Windows でのみ使用できます。

<span id="_______-rt______"></span><span id="_______-RT______"></span>**-rt**   
リアルタイムのトレースセッションを開始します。 (トレースログセッション (**-f**) が既定値です)。

**-Rt**と **-f**を使用すると、トレースメッセージがトレースコンシューマーおよびイベントトレースログファイルに送信されます。 - **Rt**または- **f**を **-バッファリング**と共に使用することはできません。 詳細については、「[トレースセッション](trace-session.md)」を参照してください。

<span id="_______-secure______"></span><span id="_______-SECURE______"></span>**-セキュリティ保護**   
保護モードでのトレースを有効にします。 このオプションは、イベント \_ トレースの \_ 保護モードのログモードを選択し \_ ます。 イベントを TRACELOG log イベントアクセス許可を持つユーザーに、セッションに記録できるユーザーを制限 \_ \_ します。

<span id="_______-sessionguid______"></span><span id="_______-SESSIONGUID______"></span>**-sessionguid**   
自動ロガーセッション GUID レジストリ値を指定します。

<span id="-SetProfInt_n_src"></span><span id="-setprofint_n_src"></span><span id="-SETPROFINT_N_SRC"></span>**-Setprofint** *n*  ****  *src*  
> [!IMPORTANT]
> プロファイル間隔を変更することはお勧めしません。

指定したソースのプロファイリング間隔 (*n*) を構成します。 *n*は100ナノ秒単位です。 既定値は 1万 (1 ミリ秒と同等) です。 このオプションは、Windows 8 以降で使用できます。

<span id="_______-seq_______MaxFileSize______"></span><span id="_______-seq_______maxfilesize______"></span><span id="_______-SEQ_______MAXFILESIZE______"></span>**-seq** *MaxFileSize*   
イベントトレースログ (.etl) ファイルへの順次ログ (ファイルの終わり、イベントの記録の停止) を指定します。 *MaxFileSize*ファイルの最大サイズを MB 単位で指定します。 *MaxFileSize*値がない場合、このパラメーターは無視されます。

既定ではシーケンシャルログが使用されますが、このパラメーターを使用して最大ファイルサイズを設定したり、 **-prealloc**を使用したりすることができます。 このパラメーターを指定しない場合、ファイルサイズの制限はありません。

<span id="_______-sourceguid________SourceGuid______"></span><span id="_______-sourceguid________sourceguid______"></span><span id="_______-SOURCEGUID________SOURCEGUID______"></span>**-sourceguid** *sourceguid*   
[Enabletraceex](https://docs.microsoft.com/windows/win32/api/evntrace/nf-evntrace-enabletraceex)または[EnableTraceEx2](https://docs.microsoft.com/windows/win32/api/evntrace/nf-evntrace-enabletraceex2)関数に*SourceId*パラメーターとして渡された GUID を指定します。 *SourceId*は、プロバイダーを有効にしたセッションを識別します。

**-stackwalk** \[*イベント*\]  
スタックを収集するカーネルイベントを指定します。 カーネルイベントの一覧を表示するには **、-Eflag Help**を使用します。 このパラメーターは、NT カーネルロガーまたはシステムロガートレースセッションに対してのみ有効です。

<span id="________________-StackWalkFilter_-in-outnid1_id2_..."></span><span id="________________-stackwalkfilter_-in-outnid1_id2_..."></span><span id="________________-STACKWALKFILTER_-IN-OUTNID1_ID2_..."></span>**-Stackウォークフィルター** {**-** | **-out***nid1} id2...*  
イベント ID フィルターに*n 個*のイベント id (許容最大64イベント id) を指定します。 このオプションは、Windows 8.1 から使用できます。

<span id="-systemlogger"></span><span id="-SYSTEMLOGGER"></span>**-systemlogger**  
Logger は SystemTraceProvider イベントを受け取ることができます。 「 [SystemTraceProvider セッションの構成と開始」を](https://docs.microsoft.com/windows/desktop/ETW/configuring-and-starting-a-systemtraceprovider-session)参照してください。 このオプションは、Windows 8 以降で使用できます。

<span id="_______-um______"></span><span id="_______-UM______"></span>**-um**   
プライベートトレースセッションを指定します。このパラメーターは、プライベートトレースセッションに必要です。

<span id="_______-UseCPUCycle______"></span><span id="_______-usecpucycle______"></span><span id="_______-USECPUCYCLE______"></span>**-UseCPUCycle**   
プロセッサの頻度 ("CPU ティック" とも呼ばれます) を使用して、各トレースメッセージの時間を計測します。

このタイマーは、可能な限り高い解決策を提供しますが、特に電源管理システムおよびマルチプロセッサコンピューターでは、エラーが発生しやすいことに注意してください。 たとえば、ARM プロセッサを搭載したコンピューターでこのタイマーを指定すると、順序が切れたイベントが発生する可能性があります。 代わりに、高解像度のトレースには **-useperfcounter**を使用することをお勧めします。

**-Useperfcounter**は、イベントトレースの既定のタイマーです。

<span id="_______-UsePerfCounter______"></span><span id="_______-useperfcounter______"></span><span id="_______-USEPERFCOUNTER______"></span>**-Useperfcounter**   
各トレースメッセージと共に、低解像度のシステム時間ではなく、高解像度のパフォーマンスカウンタークロックの値を記録します。

パフォーマンスカウンターのクロックは約100ナノ秒単位でカウントされるので、イベントごとに一意のタイムスタンプを提供します。

**-Useperfcounter**は、イベントトレースの既定のタイマーです。

<span id="_______-UseSystemTime______"></span><span id="_______-usesystemtime______"></span><span id="_______-USESYSTEMTIME______"></span>**-UseSystemTime**   
各トレースメッセージと共に、高解像度のパフォーマンスカウンターのクロック時間ではなく、システム時刻を記録します。 システムタイマーの解像度は10ミリ秒 (パフォーマンスカウンターのクロックでは100ナノ秒) であるため、複数のイベントが同じシステム時刻を持つことができます。

**-Useperfcounter**は、イベントトレースの既定のタイマーです。

<span id="_______-_____help___-_______"></span><span id="_______-_____HELP___-_______"></span>**-? | help |-?**   
使用方法に関する情報を表示します。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>Comments

次のコメントは、いくつかの Tracelog コマンドに適用されます。

### <a name="span-idsyntax_errorsspanspan-idsyntax_errorsspansyntax-errors"></a><span id="syntax_errors"></span><span id="SYNTAX_ERRORS"></span>構文エラー

Tracelog では、変更できない設定を更新しようとしたときなど、正しくない構文の組み合わせのエラーは表示されません。 代わりに、コマンドの無効な部分を無視し、成功メッセージを表示します。

### <a name="span-idsystem_loggersspanspan-idsystem_loggersspansystem-loggers"></a><span id="system_loggers"></span><span id="SYSTEM_LOGGERS"></span>システムロガー

Windows では、多くの目的でトレースセッションが使用されますが、その一部は適切な操作のために不可欠です。 開始していないトレースセッションは停止しないでください。

### <a name="span-idenumguidspanspan-idenumguidspanenumguid"></a><span id="enumguid"></span><span id="ENUMGUID"></span>Enumguid

**トレースログ start**または**トレースログ enable**コマンドが正常に実行されたかどうかを確認するには、**トレースログ-enumguid**コマンドを使用して、プロバイダーが有効になっているかどうかを確認し、**トレースログ-l (List)** コマンドを使用してトレースセッションのプロパティを確認します。

### <a name="span-idreal_time_and_log_sessionsspanspan-idreal_time_and_log_sessionsspanreal-time-and-log-sessions"></a><span id="real_time_and_log_sessions"></span><span id="REAL_TIME_AND_LOG_SESSIONS"></span>リアルタイムおよびログセッション

トレースセッションには、リアルタイムトレースセッションとトレースログセッションの両方を指定できます。 **-Rt** (リアルタイム) パラメーターと **-f** (ログセッション) パラメーターを同じコマンドに含めると、システムは、バッファーの内容をログとトレースコンシューマーの両方に送信します。 ただし、リアルタイムのメッセージ配信をトレースログセッションに追加する前に、**トレースログ-flush**コマンドを使用してバッファーをフラッシュする必要があります。

リアルタイムセッション (**-rt**) を開始してから、ログセッション (**-f**) に更新すると、新しいトレースメッセージはログファイルにのみ送信されます。 リアルタイムセッションにログファイルを追加するには、 **-rt**と **-f**の両方を**トレースログ-update**コマンドで使用します。

ログセッション (**-f**) を開始すると、リアルタイムセッション (**-rt**) に更新できますが、メッセージはトレースコンシューマーに加えて引き続きログに送信されます。 を更新することで、セッションからログを削除することはできません。

トレースメッセージをリアルタイムのみのセッションから表示または保存するには、 [Tracefmt](tracefmt.md)などのトレースコンシューマーを使用するか、トレースコントローラー (traceview など) とトレースコンシューマーの両方である[traceview](traceview.md)を使用することもできます。 Tracefmt を使用する場合は、必ず Tracefmt コマンドに **-rt**パラメーターを含めてください。

### <a name="span-idflags_and_levelsspanspan-idflags_and_levelsspanflags-and-levels"></a><span id="flags_and_levels"></span><span id="FLAGS_AND_LEVELS"></span>フラグとレベル

ほとんどのトレースプロバイダーは、フラグまたはレベルが特定の値に設定されていない限り、トレースメッセージを生成しません。 プロバイダーは、フラグまたはレベルを使用して、トレース対象を制御します。 イベントトレースログファイルが空の場合は、トレースプロバイダーのフラグとレベルを確認します。

常にトレースメッセージが生成されるようにするには、次の手順を実行します。

1.  **Flags**パラメーターを0xffffffff に設定して、すべてのフラグ設定を有効にします。

2.  **Levels**パラメーターを255に設定して、すべてのレベル設定を有効にします。

### <a name="span-idthe__eflag_parameterspanspan-idthe__eflag_parameterspanthe--eflag-parameter"></a><span id="the__eflag_parameter"></span><span id="THE__EFLAG_PARAMETER"></span>-Eflag パラメーター

Tracelog には、 **-eflag** (拡張フラグ) パラメーターがあり、 [NT カーネルロガートレースセッション](nt-kernel-logger-trace-session.md)に対して追加のフラグを有効にするように設計されています。特に、DPC、ISR、およびコンテキスト切り替えイベントのトレースを有効にするフラグです。 **トレースログ start**コマンドに **-dpcisr**パラメーターが含まれるようになったため、 **-eflag**パラメーターの使用は不要になり、推奨されません。

### <a name="span-idoutdated_parametersspanspan-idoutdated_parametersspanoutdated-parameters"></a><span id="outdated_parameters"></span><span id="OUTDATED_PARAMETERS"></span>期限切れのパラメーター

以前のバージョンのトレースログでは、**トレースログ-start**コマンドで **-rt b**パラメーターの組み合わせがサポートされていました。 この組み合わせは **-バッファリング**パラメーターに置き換えられており、無効になっています。

すべてのトレースセッションを停止するとシステムが不安定になる可能性があるため、 **-x**パラメーターは削除されました。

**-Disableex**パラメーターが削除されました。 代わりに **-disable**を使用してください。

### <a name="span-idnt_kernel_loggerspanspan-idnt_kernel_loggerspannt-kernel-logger"></a><span id="nt_kernel_logger"></span><span id="NT_KERNEL_LOGGER"></span>NT カーネルロガー

NT カーネルロガーを使用してトレースセッションを開始するには、**トレースログ-start**コマンドからセッション名を省略し、 **-guid**パラメーターを使用してプロバイダーの guid ファイルを指定しないでください。 **"NT カーネル Logger"** は、既定のセッション名です。

セッション名を省略した場合、または **"NT Kernel logger"** の場合、nt カーネルロガートレースセッションが開始されます。これは、 **-guid**パラメーターを使用して**SystemTraceControlGUID**以外の guid を指定した場合でも、nt カーネルロガートレースセッションのコントロール guid になります。 別の GUID を指定した場合、システムはエラー ("システムロガーはアプリケーション guid を受け入れません") を返しますが、NT カーネルロガートレースセッションを開始します。

既定では、Tracelog は NT カーネルロガートレースセッションを開始するときに、プロセス、スレッド、物理ディスク i/o、および TCP/IP イベントのトレースを有効にしますが、パラメーターを使用してこれらのイベントのトレースを無効にし、他のイベントのトレースを有効にすることができます。

### <a name="span-iddpc_isr_eventsspanspan-iddpc_isr_eventsspandpcisr-events"></a><span id="dpc_isr_events"></span><span id="DPC_ISR_EVENTS"></span>DPC/ISR イベント

Tracerpt では、タイムスタンプとしてシステムパフォーマンスカウンターのクロック時間が想定されているので、トレースセッションを開始するときに Tracelog **useperfcounter**パラメーターを使用します。

DPC および ISR イベントは特殊なインストルメンテーションによって収集されるため、コマンドを確認するために Tracelog に表示されるテーブルの [**有効なトレース**] 行には表示されません。

詳細については、「[例 15: DPC/ISR 時間の測定](example-15--measuring-dpc-isr-time.md)」を参照してください。
