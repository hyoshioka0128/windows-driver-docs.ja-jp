---
title: プロセスの暗黙の終了の監視
description: Windows 7 以降では、GFlags の [サイレントプロセスの終了] タブを使用して、サイレント終了を監視するプロセスの名前を入力できます。
ms.assetid: 116B2053-7F48-48B4-AEAC-333B7D9C38C7
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 809d16c8447df7ee663f8a409fd96ad6e3bd02c5
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968297"
---
# <a name="monitoring-silent-process-exit"></a>プロセスの暗黙の終了の監視


Windows 7 以降では、GFlags の [**サイレントプロセスの終了**] タブを使用して、サイレント終了を監視するプロセスの名前を入力できます。

この監視機能のコンテキストでは、"*サイレント終了*" という用語を使用して、監視対象のプロセスが次のいずれかの方法で終了することを意味します。

<span id="Self_termination"></span><span id="self_termination"></span><span id="SELF_TERMINATION"></span>自己終了  
監視対象のプロセスは、 **ExitProcess**を呼び出すことによって終了します。

<span id="Cross-process_termination"></span><span id="cross-process_termination"></span><span id="CROSS-PROCESS_TERMINATION"></span>プロセス間の終了  
2番目のプロセスでは、 **TerminateProcess**を呼び出して、監視対象のプロセスを終了します。

監視機能は、プロセスの最後のスレッドが終了したときに発生する通常のプロセス終了を検出しません。 監視機能は、カーネルモードコードによって開始されたプロセスの終了を検出しません。

サイレント終了監視のプロセスを登録するには、GFlags の [**サイレントプロセスの終了**] タブを開きます。 **画像**としてプロセス名を入力し、 **tab**キーを押します。 [**サイレントプロセス終了の監視を有効にする**] チェックボックスをオンにし、[**適用**] をクリックします。 これにより、 \_ \_ 次の \_ レジストリエントリに FLG MONITOR のサイレントプロセス終了フラグが設定され \_ ます。

**HKLM \\ SOFTWARE \\ MICROSOFT \\ Windows NT \\ CurrentVersion \\ Image File Execution Options \\ *ProcessName* \\ GlobalFlag**

このフラグの詳細については、「[サイレントプロセス終了監視の有効化](enable-silent-process-exit-monitoring.md)」を参照してください。

GFlags の [**サイレントプロセス終了**] タブの使用の詳細については、「[サイレントプロセス終了監視の構成](setting-and-clearing-flags-for-silent-process-exit.md)」を参照してください。

GFlags の [**サイレントプロセスの終了**] タブでは、監視対象プロセスがサイレントモードで終了したときに実行されるアクションを構成できます。 通知、イベントログ、およびダンプファイルの作成を構成できます。 サイレント終了が検出されたときに起動されるプロセスを指定できます。また、モニターが無視するモジュールの一覧を指定することもできます。 これらの設定のいくつかは、グローバルと個々のアプリケーションの両方で使用できます。 グローバル設定は、サイレント終了監視用に登録するすべてのプロセスに適用されます。 アプリケーション設定は個々のプロセスに適用され、グローバル設定を上書きします。

グローバル設定は、次のキーの下のレジストリに格納されます。

**HKEY \_ LOCAL \_ MACHINE \\ SOFTWARE \\ Microsoft \\ Windows NT \\ CurrentVersion \\ のコンピューター**

アプリケーション設定は、レジストリの次のキーの下に格納されます。

**HKEY \_ LOCAL \_ MACHINE \\ SOFTWARE \\ Microsoft \\ Windows NT \\ CurrentVersion ( \\ \\ ProcessName)***

## <a name="span-idreporting_modespanspan-idreporting_modespanspan-idreporting_modespanreporting-mode"></a><span id="Reporting_Mode"></span><span id="reporting_mode"></span><span id="REPORTING_MODE"></span>レポートモード


**レポートモード**設定はアプリケーション設定として使用できますが、グローバル設定としては使用できません。 レポートモードを設定するには、次のチェックボックスを使用します。

**モニタープロセス** 
 の起動**ダンプコレクション** 
 を有効にする**通知を有効にする****Reportingmode**レジストリエントリは、次のフラグのビットごとの or です。

| フラグ                   | 値 | 説明                                                                                                                                                                                            |
|------------------------|-------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| \_MONITORPROCESS の起動 | 0x1   | サイレント終了が検出されると、[**モニタープロセス**] ボックスで指定されたモニタープロセスが起動されます。                                                                                          |
| ローカル \_ ダンプ            | 0x2   | サイレント終了が検出されると、監視対象のプロセスに対してダンプファイルが作成されます。 プロセス間の終了の場合は、終了の原因となったプロセスに対してダンプファイルも作成されます。 |
| 警告           | 0x4   | サイレント終了が検出されると、ポップアップ通知が表示されます。                                                                                                                                  |

 

## <a name="span-idignore_self_exitsspanspan-idignore_self_exitsspanspan-idignore_self_exitsspanignore-self-exits"></a><span id="Ignore_Self_Exits"></span><span id="ignore_self_exits"></span><span id="IGNORE_SELF_EXITS"></span>自己終了を無視する


[**自己終了を無視**する] 設定はアプリケーション設定として使用できますが、グローバル設定としては使用できません。 [**自己終了を無視**する] チェックボックスを使用すると、自己終了を無視するかどうかを指定できます。

**Ignoreselfexits**レジストリエントリには、次のいずれかの値が含まれます。

| 値 | 説明                                                                    |
|-------|----------------------------------------------------------------------------|
| 0x0   | 自己終了とプロセス間の終了の両方を検出して対応します。 |
| 0x1   | 自己終了を無視します。 プロセス間の終了を検出して対応します。  |

 

## <a name="span-idmonitor_processspanspan-idmonitor_processspanspan-idmonitor_processspanmonitor-process"></a><span id="Monitor_Process"></span><span id="monitor_process"></span><span id="MONITOR_PROCESS"></span>プロセスの監視


[**プロセスの監視**] テキストボックスに、コマンドラインパラメーターと共にプロセス名を入力して、モニタープロセスを指定できます。 コマンドラインでは、次の変数を使用できます。

| 変数 | 説明                                                                                                                                                                                                      |
|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| % e       | プロセスの終了の ID。 これは、サイレントモードで終了した監視対象のプロセスです。                                                                                                                               |
| % i       | 開始プロセスの ID。 自己終了の場合、これは、終了プロセスと同じです。 プロセス間の終了の場合、これは終了の原因となったプロセスの ID です。 |
| % t       | 開始スレッドの ID。 これは、終了の原因となったスレッドです。                                                                                                                                  |
| % c       | **Exitthread**または**TerminateThread**に渡される状態コード。                                                                                                                                            |

 

たとえば、次の**モニタープロセス**の値は、サイレント終了時に、WinDbg が起動され、既存のプロセスにアタッチされることを指定します。

**windbg-p% e**

**監視プロセス**のコマンドラインは、 **monitorprocess**レジストリエントリに格納されます。

## <a name="span-iddump_folder_locationspanspan-iddump_folder_locationspanspan-iddump_folder_locationspandump-folder-location"></a><span id="Dump_Folder_Location"></span><span id="dump_folder_location"></span><span id="DUMP_FOLDER_LOCATION"></span>ダンプフォルダーの場所


[**ダンプフォルダーの場所**] テキストボックスを使用して、サイレント終了が検出されたときに書き込まれるダンプファイルの場所を指定できます。

**ダンプフォルダーの場所**として入力した文字列は、 **localdumpfolder**レジストリエントリに格納されます。

ダンプフォルダーの場所を指定しない場合、ダンプファイルは既定の場所 (% TEMP% サイレントプロセス終了) に書き込まれ \\ ます。

## <a name="span-iddump_folder_sizespanspan-iddump_folder_sizespanspan-iddump_folder_sizespandump-folder-size"></a><span id="Dump_Folder_Size"></span><span id="dump_folder_size"></span><span id="DUMP_FOLDER_SIZE"></span>フォルダーサイズのダンプ


[**ダンプフォルダーのサイズ**] テキストボックスを使用して、ダンプフォルダーに書き込むことができるダンプファイルの最大数を指定できます。 この値を10進整数として入力します。

**ダンプフォルダーのサイズ**として入力した値は、 **Maximumnumberofdumpfiles**レジストリエントリに格納されます。

既定では、書き込むことができるダンプファイルの数に制限はありません。

## <a name="span-iddump_typespanspan-iddump_typespanspan-iddump_typespandump-type"></a><span id="Dump_Type"></span><span id="dump_type"></span><span id="DUMP_TYPE"></span>ダンプの種類


[**ダンプの種類**] ドロップダウンリストを使用して、サイレント終了が検出されたときに書き込まれるダンプファイルの種類 (マイクロ、ミニ、ヒープ、またはカスタム) を指定できます。

ダンプの種類は**dumptype**レジストリエントリに格納されます。これは、**ミニダンプの \_ 種類**の列挙体のメンバーのビットごとの or です。 この列挙は、Windows 用デバッグツールのパッケージに含まれている dbghelp. h に定義されています。

たとえば、種類が**dump のダンプ**を選択し、 **dumptype**レジストリエントリの値が0x88 であるとします。 値0x88 は、次の2つの**ミニダンプの \_ 種類**の列挙値のビットごとの or です。

**MiniDumpFilterModulePaths**: 0x00000080

**MiniDumpFilterMemory**: 0x00000008


 

**カスタム**のダンプの種類を選択する場合は、[**カスタムダンプの種類**] ボックスに、独自の**ミニダンプの \_ 種類**の列挙値またはビットごとの or を入力します。 この値を10進整数として入力します。

## <a name="span-idmodule_ignore_listspanspan-idmodule_ignore_listspanspan-idmodule_ignore_listspanmodule-ignore-list"></a><span id="Module_Ignore_List"></span><span id="module_ignore_list"></span><span id="MODULE_IGNORE_LIST"></span>モジュール無視リスト


[**モジュールの無視**] ボックスを使用すると、サイレント終了が検出されたときに無視されるモジュールの一覧を指定できます。 監視対象のプロセスが、この一覧にあるいずれかのモジュールによって終了された場合、サイレント終了は無視されます。

[**モジュールの無視**] ボックスに入力したモジュールの一覧は、 **moduleignorelist**レジストリエントリに格納されます。

## <a name="span-idreading_process_exit_reports_in_event_viewerspanspan-idreading_process_exit_reports_in_event_viewerspanspan-idreading_process_exit_reports_in_event_viewerspanreading-process-exit-reports-in-event-viewer"></a><span id="Reading_Process_Exit_Reports_in_Event_Viewer"></span><span id="reading_process_exit_reports_in_event_viewer"></span><span id="READING_PROCESS_EXIT_REPORTS_IN_EVENT_VIEWER"></span>イベントビューアーでのプロセス終了レポートの読み取り


監視対象のプロセスがサイレントに終了すると、イベントビューアーにエントリが作成されます。 イベントビューアーを開くには、 **eventvwr**コマンドを入力します。 [ **Windows ログ] [ &gt; アプリケーション**] に移動します。 プロセス終了モニターの**ソース**を含むログエントリを探します。

![[イベントのプロパティ] ダイアログボックスの [全般] タブで、ソースがプロセス終了モニターとして表示されます。](images/gflagssilentprocessexit02.png)

 

 





