---
title: サイレント プロセス終了時の監視
description: Windows 7 以降、することができます、サイレント プロセスを終了 タブを使用 GFlags サイレントの終了を監視するプロセスの名前を入力します。
ms.assetid: 116B2053-7F48-48B4-AEAC-333B7D9C38C7
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51fdb8ff6afeb4350210b88450b1ce6ffbb5863d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537626"
---
# <a name="monitoring-silent-process-exit"></a>サイレント プロセス終了時の監視


Windows 7 以降、使える、**サイレント プロセスを終了**GFlags サイレントの終了を監視するプロセスの名前を入力するタブ。

この監視機能のコンテキストで、用語を使用します*サイレント終了*を次の方法のいずれかで、監視対象のプロセスが終了することを意味します。

<span id="Self_termination"></span><span id="self_termination"></span><span id="SELF_TERMINATION"></span>自己終了  
監視対象のプロセスは呼び出すことで終了します**ExitProcess**します。

<span id="Cross-process_termination"></span><span id="cross-process_termination"></span><span id="CROSS-PROCESS_TERMINATION"></span>プロセス間の終了  
2 番目のプロセスを呼び出して監視対象のプロセスを終了します**TerminateProcess**します。

監視機能は、プロセスの最後のスレッドが終了したときに発生する通常のプロセスの終了を検出しません。 監視機能は、カーネル モード コードによって開始されるプロセスの終了を検出しません。

サイレントの終了を監視するためのプロセスを登録するには、開く、**サイレント プロセス終了**GFlags タブ。 として、プロセス名を入力、**イメージ**キーを押すと、**タブ**キー。 チェック、**サイレント プロセス終了の監視を有効にする**ボックス、およびクリックして**適用**します。 これにより、設定、FLG\_モニター\_サイレント\_プロセス\_次のレジストリ エントリの終了フラグ。

**HKLM\\ソフトウェア\\Microsoft\\Windows NT\\CurrentVersion\\File Execution Options をイメージ\\*ProcessName* \\GlobalFlag**

このフラグの詳細については、次を参照してください。[サイレント プロセス終了の監視を有効にする](enable-silent-process-exit-monitoring.md)します。

使用しての詳細については、**サイレント プロセスの終了**GFlags でタブを参照してください[サイレント プロセス終了の監視を構成する](setting-and-clearing-flags-for-silent-process-exit.md)します。

**サイレント プロセスの終了** タブの GFlags、監視対象プロセスが自動的に終了するときに実行されるアクションを構成することができます。 通知、イベント ログ、およびダンプ ファイルの作成を構成することができます。 サイレント終了が検出されたときに起動されるプロセスを指定して、モニターが無視するモジュールの一覧を指定することができます。 これらの設定のいくつかの機能は、グローバルと個々 のアプリケーションの両方に使用できます。 グローバル設定は、サイレントの終了を監視するために登録するすべてのプロセスに適用されます。 アプリケーション設定では、個々 のプロセスに適用され、グローバル設定を上書きします。

グローバル設定は、次のキーの下のレジストリに格納されます。

**HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\Windows NT\\CurrentVersion\\SilentProcessExit**

アプリケーションの設定は、次のキーの下のレジストリに格納されます。

**HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\Windows NT\\CurrentVersion\\SilentProcessExit\\*ProcessName***

## <a name="span-idreportingmodespanspan-idreportingmodespanspan-idreportingmodespanreporting-mode"></a><span id="Reporting_Mode"></span><span id="reporting_mode"></span><span id="REPORTING_MODE"></span>報告モード


**モードの Reporting**設定が使用可能なアプリケーション設定としてではないグローバル設定です。 報告モードを設定するのには、次のチェック ボックスを使用できます。

**モニター プロセスを起動**
**ダンプの収集を有効にする**
**通知を有効にする**、 **ReportingMode**レジストリ エントリ次のフラグのビットごとの OR です。

| Flag                   | Value | 意味                                                                                                                                                                                            |
|------------------------|-------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 起動\_MONITORPROCESS | 0x1   | サイレント終了が検出されると、監視プロセス (で指定されている、**モニター プロセス**ボックス) を起動します。                                                                                          |
| ローカル\_ダンプ            | 0x2   | サイレント終了が検出されると、監視対象プロセスのダンプ ファイルが作成されます。 プロセス間の終了の場合は、終了の原因となったプロセスのダンプ ファイルを作成します。 |
| 通知           | 0x4   | サイレント終了が検出されると、ポップアップ通知が表示されます。                                                                                                                                  |

 

## <a name="span-idignoreselfexitsspanspan-idignoreselfexitsspanspan-idignoreselfexitsspanignore-self-exits"></a><span id="Ignore_Self_Exits"></span><span id="ignore_self_exits"></span><span id="IGNORE_SELF_EXITS"></span>自己終了を無視します。


**を無視する自己終了**設定が使用可能なアプリケーション設定としてではないグローバル設定です。 使用することができます、**を無視する自己終了**自己終了を無視するかどうかを指定する チェック ボックス。

**IgnoreSelfExits**レジストリ エントリは、次の値のいずれか。

| Value | 意味                                                                    |
|-------|----------------------------------------------------------------------------|
| 0x0   | 検出し、自己終了と終了のプロセス間の両方に対応します。 |
| 0x1   | 自己終了を無視します。 検出し、プロセス間の終了に対応します。  |

 

## <a name="span-idmonitorprocessspanspan-idmonitorprocessspanspan-idmonitorprocessspanmonitor-process"></a><span id="Monitor_Process"></span><span id="monitor_process"></span><span id="MONITOR_PROCESS"></span>プロセスの監視


モニター プロセスを指定するにはでコマンドラインのパラメーターと共に、プロセス名を入力して、**モニター プロセス**テキスト ボックス。 コマンドラインで、次の変数を使用することができます。

| 変数を用意 | 意味                                                                                                                                                                                                      |
|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| %e       | 既存のプロセスの ID。 これは、監視対象のプロセスをサイレント モードで終了しました。                                                                                                                               |
| %i       | 発信側のプロセスの ID。 自己終了の場合これは、既存のプロセスと同じです。 プロセス間の終了の場合これは、終了の原因となったプロセスの ID です。 |
| %t       | 発信側のスレッドの ID。 これは、終了の原因となったスレッドです。                                                                                                                                  |
| %c       | 渡される状態コード**ExitThread**または**TerminateThread**します。                                                                                                                                            |

 

場合、次の値など、**モニター プロセス**をサイレント終了時に、WinDbg が起動し、既存のプロセスにアタッチされているを指定します。

**windbg -p %e**

**モニター プロセス**にコマンドラインが格納されている、 **MonitorProcess**レジストリ エントリ。

## <a name="span-iddumpfolderlocationspanspan-iddumpfolderlocationspanspan-iddumpfolderlocationspandump-folder-location"></a><span id="Dump_Folder_Location"></span><span id="dump_folder_location"></span><span id="DUMP_FOLDER_LOCATION"></span>フォルダーの場所をダンプします。


使用することができます、**フォルダーの場所をダンプ**テキスト ボックスに、サイレントの終了が検出されたときに書き込まれる、ダンプ ファイルの場所を指定します。

用に入力した文字列**フォルダーの場所をダンプ**に格納されている場合は、 **LocalDumpFolder**レジストリ エントリ。

ダンプ フォルダーの場所を指定しない場合、ダンプ ファイルは %temp% は、既定の場所に書き込まれます\\サイレント プロセスが終了します。

## <a name="span-iddumpfoldersizespanspan-iddumpfoldersizespanspan-iddumpfoldersizespandump-folder-size"></a><span id="Dump_Folder_Size"></span><span id="dump_folder_size"></span><span id="DUMP_FOLDER_SIZE"></span>ダンプのフォルダのサイズ


使用することができます、**フォルダーのサイズをダンプ**ファイルをダンプの最大数を指定するテキスト ボックスは、ダンプのフォルダに書き込むことができます。 10 進整数としてこの値を入力します。

用に入力した値**フォルダーのサイズをダンプ**に格納されている場合は、 **MaximumNumberOfDumpFiles**レジストリ エントリ。

既定では、書き込むことのできるダンプ ファイルの数に制限はありません。

## <a name="span-iddumptypespanspan-iddumptypespanspan-iddumptypespandump-type"></a><span id="Dump_Type"></span><span id="dump_type"></span><span id="DUMP_TYPE"></span>ダンプの種類


使用することができます、**ダンプの種類**サイレント終了が検出されたときに記述されたダンプ ファイル (Micro、Mini、ヒープ、またはカスタム) の種類を指定するドロップダウン リスト。

ダンプの種類は、 **DumpType**はビットごとのレジストリ エントリまたはのメンバーの**ミニダンプ\_型**列挙体。 この列挙体は、Windows のツールをデバッグ パッケージに含まれている dbghelp.h で定義されます。

たとえばのダンプの種類を選択した**マイクロ**、ことを確認して、 **DumpType**レジストリ エントリは 0x88 の値を持ちます。 0x88 値は次の 2 つのビットごとの OR**ミニダンプ\_型**列挙値。

|                           |            |
|---------------------------|------------|
| MiniDumpFilterModulePaths | 0x00000080 |
| MiniDumpFilterMemory      | 0x00000008 |

 

ダンプの種類を選択した場合**カスタム**、独自のビットごとの OR の入力**ミニダンプ\_型**列挙の値で、**ダンプの種類のカスタム**ボックス。 10 進整数としてこの値を入力します。

## <a name="span-idmoduleignorelistspanspan-idmoduleignorelistspanspan-idmoduleignorelistspanmodule-ignore-list"></a><span id="Module_Ignore_List"></span><span id="module_ignore_list"></span><span id="MODULE_IGNORE_LIST"></span>モジュール一覧を無視します。


使用することができます、**モジュール無視リスト**サイレント終了が検出されたときに無視されるモジュールの一覧を指定するボックスです。 監視対象のプロセスが終了した場合、モジュールの一覧のいずれかで、サイレントの終了は無視されます。

入力するモジュールの一覧、**モジュール無視リスト**にボックスが格納されている、 **ModuleIgnoreList**レジストリ エントリ。

## <a name="span-idreadingprocessexitreportsineventviewerspanspan-idreadingprocessexitreportsineventviewerspanspan-idreadingprocessexitreportsineventviewerspanreading-process-exit-reports-in-event-viewer"></a><span id="Reading_Process_Exit_Reports_in_Event_Viewer"></span><span id="reading_process_exit_reports_in_event_viewer"></span><span id="READING_PROCESS_EXIT_REPORTS_IN_EVENT_VIEWER"></span>イベント ビューアーでレポートの読み取り処理終了


監視対象のプロセスが自動的に終了すると、モニターは、イベント ビューアーでエントリを作成します。 イベント ビューアーを開くには、コマンドを入力**eventvwr.msc**します。 移動します**Windows ログ&gt;アプリケーション**します。 持つログ エントリを探して、**ソース**のプロセス終了のモニター。

![イベントのプロパティ ダイアログ ボックスが表示された 全般 タブ プロセス終了のモニターとしてソースを表示します。](images/gflagssilentprocessexit02.png)

 

 





