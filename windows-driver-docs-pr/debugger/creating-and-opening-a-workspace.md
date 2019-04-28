---
title: ワークスペースを作成して開く
description: ワークスペースを作成して開く
ms.assetid: 0163f380-f982-4635-a450-ed83f0b52e03
keywords:
- ワークスペースを作成します。
- ワークスペースを開く
- ワークスペースをという名前のワークスペース
- ワークスペースでは、既定のワークスペース
- ワークスペースでは、ワークスペースの種類
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11cd78591bfa934f4ac7f7ee7dcb2760d6641b70
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375464"
---
# <a name="creating-and-opening-a-workspace"></a>ワークスペースを作成して開く


## <span id="ddk_creating_and_opening_a_workspace_dbg"></span><span id="DDK_CREATING_AND_OPENING_A_WORKSPACE_DBG"></span>


WinDbg はワークスペースの 2 つの種類:*既定のワークスペース*と*という名前のワークスペース*します。

### <a name="span-iddefaultworkspacesspanspan-iddefaultworkspacesspandefault-workspaces"></a><span id="default_workspaces"></span><span id="DEFAULT_WORKSPACES"></span>既定のワークスペース

WinDbg では、既定のワークスペースのさまざまな種類があります。

-   *基本ワークスペース*WinDbg が休止状態のときに使用します。

-   *の既定のユーザー モード ワークスペース*ユーザー モード プロセスにアタッチするときに使用されます (を使用して、 **-p**[**コマンド ライン オプション**](windbg-command-line-options.md)またはを使用して、[ファイル |プロセスにアタッチする](file---attach-to-a-process.md)コマンド)。

-   *リモートの既定のワークスペース*デバッグ サーバーに接続するときに使用されます。

-   *の既定のカーネル モード ワークスペース*WinDbg カーネル モードのデバッグ セッションを開始するときに使用されます。

-   *プロセッサ固有ワークスペース*WinDbg がターゲット コンピューターに接続した後のカーネル モードのデバッグ中に使用されます。 X86 ベースおよび x64 ベース プロセッサの個別のプロセッサ固有ワークスペースがあります。

WinDbg では、デバッグ用のユーザー モード プロセスを作成するときは、その実行可能ファイルのワークスペースが作成されます。 各作成された実行可能ファイルには、独自のワークスペースがあります。

WinDbg は、ダンプ ファイルを分析し、そのダンプ ファイルの分析セッションのワークスペースが作成されます。 各ダンプ ファイルには、独自のワークスペースがあります。

デバッグ セッションを開始するときに、適切なワークスペースが読み込まれます。 デバッグ セッションを終了するか、WinDbg を終了すると、ときにダイアログ ボックスが表示され、現在のワークスペースに加えた変更を保存するように要求。 WinDbg を開始する場合、 **- QY**[**コマンド ライン オプション**](windbg-command-line-options.md)、このダイアログ ボックスが表示されないと、ワークスペースが自動的に保存します。 また、WinDbg でを起動する場合、 **-q**コマンド ライン オプションは、このダイアログ ボックスが表示されないと、変更は保存されません。

ワークスペースは、累積的な方法で読み込みます。 ベースのワークスペースは、最初に常に読み込まれます。 特定のデバッグ操作を開始するときに、適切なワークスペースが読み込まれます。 2 つのワークスペースが読み込まれた後、そのほとんどのデバッグ処理が完了しました。 (ベースのワークスペース、既定のカーネル モード ワークスペース、およびプロセッサ固有ワークスペース) 3 つのワークスペースが読み込まれた後、カーネル モードのデバッグ処理が完了しました。

WinDbg 作業のすべてに適用する場合、最大の効率は下位レベルのワークスペースでの設定を保存してください。

**注**  デバッグ情報のウィンドウのレイアウトは、ワークスペースの累積的な動作を 1 つの例外。 開いて最新のワークスペースのみによっては、位置、ドッキング状態、および各ウィンドウのサイズが決まります。 この動作には、[ウォッチ] ウィンドウとそれぞれに表示した場所の内容が含まれています。[メモリ ウィンドウ](memory-window.md)します。 コマンド履歴に、[デバッガー コマンド ウィンドウ](debugger-command-window.md)はクリアされない新しいワークスペースを開くが、他のすべてのウィンドウの状態がリセットされます。

 

基本のワークスペースにアクセスするターゲットなしの WinDbg を起動するかクリックして[デバッグの停止](debug---stop-debugging.md)上、**デバッグ**セッションが完了した後のメニュー。 基本のワークスペースで使用できる任意の編集を行うことができます。

### <a name="span-idnamedworkspacesspanspan-idnamedworkspacesspannamed-workspaces"></a><span id="named_workspaces"></span><span id="NAMED_WORKSPACES"></span>名前付きのワークスペース

ワークスペースの名前を付けると、保存したり、読み込むには個別にできます。 名前付きのワークスペースの読み込み後、すべての自動読み込みと既定のワークスペースの保存が無効です。

名前付きのワークスペースには、既定のワークスペースにはないいくつかの追加情報が含まれて。 この追加情報の詳細については、次を参照してください。[ワークスペース内容](workspace-contents.md)します。

### <a name="span-idopeningsavingandclearingworkspacesspanspan-idopeningsavingandclearingworkspacesspanopening-saving-and-clearing-workspaces"></a><span id="opening__saving__and_clearing_workspaces"></span><span id="OPENING__SAVING__AND_CLEARING_WORKSPACES"></span>開く、保存、およびワークスペースをクリアします。

ワークスペースを制御するには、次の操作を行うことができます。

-   使用して名前付きのワークスペースを読み込むを開き、 **-w** [**コマンド ライン オプション**](windbg-command-line-options.md)します。

-   ワークスペースを使用して、ファイルから読み込むを開き、 **-WF** [**コマンド ライン オプション**](windbg-command-line-options.md)します。

-   すべての自動のワークスペースを使用して読み込みを無効にする、 **-WX** [**コマンド ライン オプション**](windbg-command-line-options.md)します。 明示的ワークスペース コマンドのみを保存したり、読み込まれたワークスペースが発生します。

-   開き、クリックして名前付きのワークスペースを読み込む[ワークスペースを開く](file---open-workspace.md)上、**ファイル**メニューまたは CTRL + W キーを押します。

-   現在の既定のワークスペースまたは名前付きの現在のワークスペースをクリックして保存[ワークスペースの保存](file---save-workspace.md)上、**ファイル**メニュー。

-   現在のワークスペースに名前を割り当てるし、クリックして保存[ワークスペースに名前を付けて](file---save-workspace-as.md)上、**ファイル**メニュー。

-   特定のアイテムおよび設定をクリックして、現在のワークスペースから削除[クリア ワークスペース](file---clear-workspace.md)上、**ファイル**メニュー。

-   ワークスペースをクリックして削除[ワークスペースの削除](file---delete-workspaces.md)上、**ファイル**メニュー。

-   開き、ワークスペースをクリックしてファイルから読み込む[ファイルでワークスペースを開く](file---open-workspace-in-file.md)上、**ファイル**メニュー。

-   ワークスペースをクリックしてファイルに保存[ファイルに保存](file---save-workspace-to-file.md)上、**ファイル**メニュー。

 

 





