---
title: Windows 用デバッグ ツールに含まれるツール
description: デバッグ ツールの Windows には、デバッグ エンジンとデバッグ環境だけでなく、いくつかのツールが含まれています。 このツールはツールを Windows のデバッグのインストール ディレクトリです。
ms.assetid: f5d761b9-866e-4948-978e-e95f8aed8b21
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ac79b379f2c1ea9221070f250af9a1b8d44cd84
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529760"
---
# <a name="tools-included-in-debugging-tools-for-windows"></a>Windows 用デバッグ ツールに含まれるツール


デバッグ ツールの Windows デバッグ エンジンだけでなく、いくつかのツールが含まれていますと[デバッグ環境](debuggers-in-the-debugging-tools-for-windows-package.md)します。 このツールは、[インストール ディレクトリ](#installation-directories)の Windows のツールをデバッグします。

## <span id="additional_tools_and_utilities"></span><span id="ADDITIONAL_TOOLS_AND_UTILITIES"></span>


<span id="ADPlus"></span><span id="adplus"></span><span id="ADPLUS"></span>[ADPlus](adplus.md)  
自動的にメモリ ダンプ ファイルを作成し、1 つまたは複数のプロセスからのデバッグ出力とログ ファイル。

<span id="DumpChk"></span><span id="dumpchk"></span><span id="DUMPCHK"></span>[DumpChk](dumpchk.md)  
メモリ ダンプ ファイルを検証します。

<span id="GFlags"></span><span id="gflags"></span><span id="GFLAGS"></span>[GFlags](gflags.md)  
レジストリ キーとその他の設定を制御します。

<span id="Kill"></span><span id="kill"></span><span id="KILL"></span>[Kill](kill-tool.md)  
プロセスを終了します。

<span id="Logger_and_LogViewer"></span><span id="logger_and_logviewer"></span><span id="LOGGER_AND_LOGVIEWER"></span>[Logger と LogViewer](logger-and-logviewer.md)  
記録し、関数呼び出しと、プログラムの他のアクションを表示します。

<span id="PLMDebug"></span><span id="plmdebug"></span><span id="PLMDEBUG"></span>[PLMDebug](plmdebug.md)  
プロセス ライフ サイクル管理 (PLM) の下を実行する Windows のアプリをデバッグするのにには、Windows デバッガーを使用します。 PLMDebug、中断、再開、および Windows アプリを終了して手動で制御するができます。

<span id="Remote_Tool"></span><span id="remote_tool"></span><span id="REMOTE_TOOL"></span>[リモート ツール](remote-tool.md)  
KD、CDB、NTSD など、任意のコンソール プログラムをリモートで制御します。 参照してください[Remote.exe を通じてリモート デバッグ](remote-debugging-through-remote-exe.md)します。

<span id="TList"></span><span id="tlist"></span><span id="TLIST"></span>[TList](tlist.md)  
すべての実行中のプロセスを一覧表示します。

<span id="UMDH"></span><span id="umdh"></span>[UMDH](umdh.md)  
ヒープの割り当てを分析します。

<span id="USBView"></span><span id="usbview"></span><span id="USBVIEW"></span>[USBView](usbview.md)  
USB ホスト コント ローラーと接続されたデバイスを表示します。

<span id="dbgrpc___dbgrpc.exe_"></span><span id="DBGRPC___DBGRPC.EXE_"></span>させるため (Dbgrpc.exe)  
Microsoft リモート プロシージャ コール (RPC) の状態情報を表示します。 参照してください[RPC デバッグ](rpc-debugging.md)と[させるためのツールを使用して](using-the-dbgrpc-tool.md)します。

<span id="kdbgctrl___kernel_debugging_control__kdbgctrl.exe_"></span><span id="KDBGCTRL___KERNEL_DEBUGGING_CONTROL__KDBGCTRL.EXE_"></span>KDbgCtrl (Kernel Debugging Control, Kdbgctrl.exe)  
制御し、カーネル デバッグ接続を構成します。 参照してください[KDbgCtrl を使用して](using-kdbgctrl.md)します。

<span id="SrcSrv"></span><span id="srcsrv"></span><span id="SRCSRV"></span>[SrcSrv](srcsrv.md)  
移行元サーバーのデバッグ中にソース ファイルを配信するために使用できます。

<span id="SymSrv"></span><span id="symsrv"></span><span id="SYMSRV"></span>[SymSrv](symsrv.md)  
デバッガーがシンボル ストアへの接続に使用できるシンボル サーバー。

<span id="SymProxy"></span><span id="symproxy"></span><span id="SYMPROXY"></span>[SymProxy](symproxy.md)  
すべてのデバッガーを指すことができます、ネットワーク上の 1 つの HTTP シンボル サーバーを作成します。 これは、シンボルによる複数のサーバー (内部および外部の両方)、1 つのシンボルのパスをポイントし、すべての認証を処理して、シンボルのキャッシュによるパフォーマンスの向上のメリットがあります。 Symproxy.dll が SymProxy フォルダーには、[インストール ディレクトリ](#installation-directories)します。

<span id="SymChk"></span><span id="symchk"></span><span id="SYMCHK"></span>[SymChk](symchk.md)  
適切なシンボルが使用できることを確認するシンボル ファイルの実行可能ファイルを比較します。

<span id="SymStore"></span><span id="symstore"></span><span id="SYMSTORE"></span>[SymStore](symstore.md)  
シンボル ストアを作成します。 参照してください[SymStore を使用して](symstore.md)します。

<span id="AgeStore"></span><span id="agestore"></span><span id="AGESTORE"></span>[AgeStore](agestore.md)  
シンボル サーバーまたは移行元サーバーのダウン ストリームのストア内の古いエントリを削除します。

<span id="DBH"></span><span id="dbh"></span>[DBH](dbh.md)  
シンボル ファイルの内容に関する情報を表示します。

<span id="PDBCopy"></span><span id="pdbcopy"></span><span id="PDBCOPY"></span>[PDBCopy](pdbcopy.md)  
シンボル ファイルからプライベート シンボル情報を削除し、ファイルのどのパブリック シンボルを制御します。

<span id="DbgSrv__"></span><span id="dbgsrv__"></span><span id="DBGSRV__"></span>DbgSrv   
プロセス サーバーのリモート デバッグに使用します。 参照してください[プロセス サーバー (ユーザー モード)](process-servers--user-mode-.md)します。

<span id="KdSrv"></span><span id="kdsrv"></span><span id="KDSRV"></span>KdSrv  
KD 接続サーバーのリモート デバッグに使用します。参照してください[KD 接続サーバー (カーネル モード)](kd-connection-servers--kernel-mode-.md)します。

<span id="DbEngPrx"></span><span id="dbengprx"></span><span id="DBENGPRX"></span>DbEngPrx  
リモート デバッグに使用 repeater (小規模なプロキシ サーバー)。 参照してください[リピータ](repeaters.md)します。

<span id="breakin___breakin.exe_"></span><span id="BREAKIN___BREAKIN.EXE_"></span>侵入 (Breakin.exe)  
プロセスで発生するユーザー モード区切りが発生します。 ヘルプについては、コマンド プロンプト ウィンドウを開きに移動、[インストール ディレクトリ](#installation-directories)、入力と**侵入/でしょうか。**。

<span id="list___file_list_utility___list.exe_"></span><span id="LIST___FILE_LIST_UTILITY___LIST.EXE_"></span>一覧 (ファイルの一覧ユーティリティ) (List.exe)  
ヘルプについては、コマンド プロンプト ウィンドウを開きに移動します、[インストール ディレクトリ](#installation-directories)、入力と**リスト/でしょうか。** します。

<span id="rtlist___remote_task_list_viewer___rtlist.exe_"></span><span id="RTLIST___REMOTE_TASK_LIST_VIEWER___RTLIST.EXE_"></span>RTList (リモート タスク リスト ビューアー) (Rtlist.exe)  
DbgSrv プロセス サーバーを経由して実行中のプロセスを一覧表示します。 ヘルプについては、コマンド プロンプト ウィンドウを開きに移動、[インストール ディレクトリ](#installation-directories)、入力と**rtlist/でしょうか。**。

## <a name="span-idinstallation-directoriesspanspan-idinstallation-directoriesspaninstallation-directory"></a><span id="installation-directories"></span><span id="INSTALLATION-DIRECTORIES"></span>インストール ディレクトリ


デバッグ ツールの 64 ビットの OS のインストールの既定のインストール ディレクトリは、c:\\Program Files (x86)\\Windows キット\\10\\デバッガー\\します。 C: Windows キット フォルダーを見つけることができます、32 ビット OS があれば、\\プログラム ファイル。 かどうかは、32 ビットまたは 64 ビットのツールを使用する必要がありますを確認するのを参照してください。 [32 ビットまたは 64 ビット デバッグ ツールを選択する](choosing-a-32-bit-or-64-bit-debugger-package.md)します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Windows 用デバッグ ツールに関連するツール](tools-related-to-debugging-tools-for-windows.md)

 

 






