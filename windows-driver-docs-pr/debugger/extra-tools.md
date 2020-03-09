---
title: Debugging Tools for Windows に含まれるツール
description: Windows 用デバッグツールには、デバッグエンジンやデバッグ環境に加えて、いくつかのツールが含まれています。 ツールは、Windows 用デバッグツールのインストールディレクトリにあります。
ms.assetid: f5d761b9-866e-4948-978e-e95f8aed8b21
ms.date: 12/03/2019
ms.localizationpriority: medium
ms.openlocfilehash: 819c50b37d14a228af0d00da4678b05230fbabcb
ms.sourcegitcommit: e1cfed28850a8208ea27e7a6a336de88c48e9948
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78402412"
---
# <a name="tools-included-in-debugging-tools-for-windows"></a>Debugging Tools for Windows に含まれるツール

Windows 用デバッグツールには、デバッグエンジンや[デバッグ環境](debuggers-in-the-debugging-tools-for-windows-package.md)に加えて、いくつかのツールが含まれています。 ツールは、Windows 用デバッグツールの[インストールディレクトリ](#installation-directories)にあります。

## <span id="additional_tools_and_utilities"></span><span id="ADDITIONAL_TOOLS_AND_UTILITIES"></span>

<span id="DumpChk"></span><span id="dumpchk"></span><span id="DUMPCHK"></span>[DumpChk](dumpchk.md)  
メモリダンプファイルを検証します。

<span id="GFlags"></span><span id="gflags"></span><span id="GFLAGS"></span>[Flag](gflags.md)  
レジストリキーおよびその他の設定を制御します。

<span id="Kill"></span><span id="kill"></span><span id="KILL"></span>[停止](kill-tool.md)  
プロセスを終了します。

<span id="Logger_and_LogViewer"></span><span id="logger_and_logviewer"></span><span id="LOGGER_AND_LOGVIEWER"></span>[Logger および LogViewer](logger-and-logviewer.md)  
プログラムの関数呼び出しやその他のアクションを記録して表示します。

<span id="PLMDebug"></span><span id="plmdebug"></span><span id="PLMDEBUG"></span>[PLMDebug](plmdebug.md)  
Windows デバッガーを使用して、プロセスライフサイクル管理 (PLM) で実行される Windows アプリをデバッグします。 PLMDebug を使用すると、Windows アプリの中断、再開、および終了を手動で制御できます。

<span id="Remote_Tool"></span><span id="remote_tool"></span><span id="REMOTE_TOOL"></span>[リモートツール](remote-tool.md)  
KD、CDB、NTSD など、任意のコンソールプログラムをリモートで制御します。 「リモート[デバッグ](remote-debugging-through-remote-exe.md)」を参照してください。

<span id="TList"></span><span id="tlist"></span><span id="TLIST"></span>[Tlist.exe](tlist.md)  
実行中のすべてのプロセスを一覧表示します。

<span id="UMDH"></span><span id="umdh"></span>[UMDH](umdh.md)  
ヒープ割り当てを分析します。

<span id="USBView"></span><span id="usbview"></span><span id="USBVIEW"></span>[USBView](usbview.md)  
USB ホストコントローラーと接続されているデバイスを表示します。

<span id="dbgrpc___dbgrpc.exe_"></span><span id="DBGRPC___DBGRPC.EXE_"></span>DbgRpc (Dbgrpc .exe)  
Microsoft リモートプロシージャコール (RPC) の状態情報を表示します。 「 [RPC デバッグ](rpc-debugging.md)」および「 [Dbgrpc ツールの使用](using-the-dbgrpc-tool.md)」を参照してください。

<span id="kdbgctrl___kernel_debugging_control__kdbgctrl.exe_"></span><span id="KDBGCTRL___KERNEL_DEBUGGING_CONTROL__KDBGCTRL.EXE_"></span>KDbgCtrl (カーネルデバッグコントロール、Kdbgctrl .exe)  
カーネルデバッグ接続を制御および構成します。 「 [KDbgCtrl の使用」を](using-kdbgctrl.md)参照してください。

<span id="SrcSrv"></span><span id="srcsrv"></span><span id="SRCSRV"></span>[SrcSrv](srcsrv.md)  
デバッグ中にソースファイルを配信するために使用できるソースサーバー。

<span id="SymSrv"></span><span id="symsrv"></span><span id="SYMSRV"></span>[SymSrv](symsrv.md)  
シンボルストアに接続するためにデバッガーが使用できるシンボルサーバー。

<span id="SymProxy"></span><span id="symproxy"></span><span id="SYMPROXY"></span>[SymProxy](symproxy.md)  
すべてのデバッガーが参照できる単一の HTTP シンボルサーバーをネットワーク上に作成します。 これには、1つのシンボルパスを使用して複数のシンボルサーバー (内部と外部の両方) をポイントし、すべての認証を処理し、シンボルキャッシュによってパフォーマンスを向上させるという利点があります。 Symproxy .dll は、[インストールディレクトリ](#installation-directories)の symproxy フォルダーにあります。

<span id="SymChk"></span><span id="symchk"></span><span id="SYMCHK"></span>[SymChk](symchk.md)  
実行可能ファイルをシンボルファイルと比較して、正しいシンボルが使用可能であることを確認します。

<span id="SymStore"></span><span id="symstore"></span><span id="SYMSTORE"></span>[SymStore](symstore.md)  
シンボルストアを作成します。 「 [Using SymStore」を](symstore.md)参照してください。

<span id="AgeStore"></span><span id="agestore"></span><span id="AGESTORE"></span>[AgeStore](agestore.md)  
シンボルサーバーまたはソースサーバーの下流ストア内の古いエントリを削除します。

<span id="DBH"></span><span id="dbh"></span>[DBH](dbh.md)  
シンボルファイルの内容に関する情報を表示します。

<span id="PDBCopy"></span><span id="pdbcopy"></span><span id="PDBCOPY"></span>[PDBCopy](pdbcopy.md)  
シンボルファイルからプライベートシンボル情報を削除し、ファイルに含めるパブリックシンボルを制御します。

<span id="DbgSrv__"></span><span id="dbgsrv__"></span><span id="DBGSRV__"></span>DbgSrv   
リモートデバッグに使用されるプロセスサーバー。 「[プロセスサーバー (ユーザーモード)](process-servers--user-mode-.md)」を参照してください。

<span id="KdSrv"></span><span id="kdsrv"></span><span id="KDSRV"></span>KdSrv  
リモートデバッグに使用される KD 接続サーバー。「 [KD 接続サーバー (カーネルモード)](kd-connection-servers--kernel-mode-.md)」を参照してください。

<span id="DbEngPrx"></span><span id="dbengprx"></span><span id="DBENGPRX"></span>DbEngPrx  
リモートデバッグに使用されるリピータ (s プロキシサーバー)。 「[リピータ](repeaters.md)」を参照してください。

<span id="breakin___breakin.exe_"></span><span id="BREAKIN___BREAKIN.EXE_"></span>侵入 (侵入)  
プロセスでユーザーモードの中断を発生させます。 ヘルプを表示するには、コマンドプロンプトウィンドウを開き、[インストールディレクトリ](#installation-directories)に移動して、「**侵入/?** 」と入力します。

<span id="list___file_list_utility___list.exe_"></span><span id="LIST___FILE_LIST_UTILITY___LIST.EXE_"></span>List (ファイルリストユーティリティ) (List .exe)  
ヘルプを表示するには、コマンドプロンプトウィンドウを開き、[インストールディレクトリ](#installation-directories)に移動して、「 **list/?** 」と入力します。

<span id="rtlist___remote_task_list_viewer___rtlist.exe_"></span><span id="RTLIST___REMOTE_TASK_LIST_VIEWER___RTLIST.EXE_"></span>RTList (リモートタスク一覧ビューアー) (Rtlist .exe)  
DbgSrv プロセスサーバーを介して実行中のプロセスを一覧表示します。 ヘルプを表示するには、コマンドプロンプトウィンドウを開き、[インストールディレクトリ](#installation-directories)に移動して、「 **rtlist/?** 」と入力します。

## <a name="span-idinstallation-directoriesspanspan-idinstallation-directoriesspaninstallation-directory"></a><span id="installation-directories"></span><span id="INSTALLATION-DIRECTORIES"></span>インストールディレクトリ

デバッグツール用の64ビット OS インストールの既定のインストールディレクトリは、C:\\Program Files (x86)\\Windows キット\\10\\デバッガー\\です。 32ビットの OS を使用している場合は、[C:\\Program Files] の下にある Windows Kit フォルダーを見つけることができます。 32ビットまたは64ビットのツールを使用する必要があるかどうかを判断するには、「 [32 ビットまたは64ビットのデバッグツールの選択](choosing-a-32-bit-or-64-bit-debugger-package.md)」を参照してください。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック

[Windows 用のデバッグツールに関連するツール](tools-related-to-debugging-tools-for-windows.md)
