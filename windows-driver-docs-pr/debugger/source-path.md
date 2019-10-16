---
title: ソース パス
description: このトピックでは、ソースパスを設定する方法、または個々のソースファイルを読み込む方法について説明します。
ms.assetid: b5dcb557-b413-401a-be4b-2d45b2597e6c
keywords: ソースファイルとパス、ソースパス
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 686870221ff72a5ecf60cd8a56c18c32bf97302d
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72323595"
---
# <a name="source-path"></a>ソース パス


## <span id="ddk_source_path_dbg"></span><span id="DDK_SOURCE_PATH_DBG"></span>


*ソースパス*では、C ファイルとC++ソースファイルが配置されているディレクトリを指定します。

実行可能ファイルがビルドされたコンピューターでユーザーモードプロセスをデバッグしていて、ソースファイルが依然として元の場所にある場合、デバッガーは自動的にソースファイルを検索できます。

その他の状況では、ソースパスを設定するか、個々のソースファイルを読み込む必要があります。

デバッガーを使用し[てリモートデバッグ](remote-debugging-through-the-debugger.md)を実行する場合、デバッグサーバーはソースパスを使用します。 デバッガーとして WinDbg を使用している場合は、各デバッグクライアントにも独自の*ローカルソースパス*があります。 ソース関連のすべてのコマンドは、ローカルコンピューター上のソースファイルにアクセスします。 ソースコマンドを使用するすべてのクライアントまたはサーバーで、適切なパスを設定する必要があります。

このマルチパスシステムを使用すると、デバッグクライアントは、ソースファイルを他のクライアントやサーバーと共有しなくても、ソース関連のコマンドを使用できます。 このシステムは、1人のユーザーがアクセスできるプライベートまたは機密のソースファイルがある場合に便利です。

ソースパスに関係なく、いつでもソースファイルを読み込むことができます。

### <a name="span-idsource_path_syntaxspanspan-idsource_path_syntaxspansource-path-syntax"></a><span id="source_path_syntax"></span><span id="SOURCE_PATH_SYNTAX"></span>ソースパスの構文

デバッガーのソースパスは、セミコロンで区切られた複数のディレクトリパスで構成される文字列です。

相対パスがサポートされています。 ただし、常に同じディレクトリからデバッガーを起動する場合を除き、各パスの前にドライブ文字またはネットワーク共有を追加する必要があります。 ネットワーク共有もサポートされています。

**メモ**  企業ネットワークに接続している場合、ソースファイルにアクセスする最も効率的な方法は、移行元サーバーを使用することです。 ソースパス内で**srv @ no__t*** 文字列を使用して、移行元サーバーを使用できます。 ソースサーバーの詳細については、「[ソースサーバーの使用](using-a-source-server.md)」を参照してください。

 

### <a name="span-idcontrolling_the_source_pathspanspan-idcontrolling_the_source_pathspancontrolling-the-source-path"></a><span id="controlling_the_source_path"></span><span id="CONTROLLING_THE_SOURCE_PATH"></span>ソースパスの制御

ソースパスとローカルソースパスを制御するには、次のいずれかの操作を行います。

-   デバッガーを開始する前に、\_NT @ no__t-1SOURCE @ no__t-2PATH[環境変数](environment-variables.md)を使用して、ソースパスを設定します。 この環境変数を使用して無効なディレクトリを追加しようとすると、デバッガーはこのディレクトリを無視します。

-   デバッガーを起動するときに、 **-srcpath**[コマンドラインオプション](command-line-options.md)を使用してソースパスを設定します。

-   ソースパスを表示、設定、変更、または追加するには、 [ **. srcpath (ソースパスの設定)** ](-srcpath---lsrcpath--set-source-path-.md)コマンドを使用します。 移行元サーバーを使用している場合、 [ **(ソースサーバーを使用して) srcfix**](-srcfix---lsrcfix--use-source-server-.md)は少し簡単になります。

-   (WinDbg のみ)[**Lsrcpath (ローカルソースパスの設定)** ](-srcpath---lsrcpath--set-source-path-.md)コマンドを使用して、ローカルソースパスを表示、設定、変更、または追加します。 移行元サーバーを使用している場合は、 [**lsrcfix (ローカルソースサーバーを使用)** ](-srcfix---lsrcfix--use-source-server-.md)が少し簡単になります。 また、lscrpath パラメーターを指定して WinDbg コマンドラインを使用することもできます。 詳細については、「 [**WinDbg のコマンドラインオプション**](windbg-command-line-options.md)」を参照してください。

-   (WinDbg のみ)File | を使用します。 [[ソースファイルのパス](file---source-file-path.md)] コマンドを押すか、CTRL キーを押しながら P キーを押して、ソースパスまたはローカルソースパスを表示、設定、変更、または追加します。

また、次のいずれかを実行して、ソースファイルを直接開いたり閉じたりすることもできます。

-   [**Lsf (ソースファイルの読み込みまたはアンロード)** ](lsf--lsf---load-or-unload-source-file-.md)コマンドを使用して、ソースファイルを開いたり閉じたりします。

-   (WinDbg のみ)開く[ **(ソースファイルを開く)** ](-open--open-source-file-.md)コマンドを使用して、ソースファイルを開きます。

-   (WinDbg のみ)[File | open source file](file---open-source-file.md)コマンドを使用するか、ctrl + o キーを押してソースファイルを開きます。 また @no__t、ツールバーの [ソースファイルを開く] をクリックすると、[オープンソースファイル] ボタン @ no__t のスクリーンショットが**表示され**ます。

    File | を使用すると    に**注意**してください。 **ソースファイル (また**はそのショートカットメニューまたは同等のボタン) を開いてソースファイルを開くと、そのファイルのパスがソースパスに自動的に追加されます。

     

-   (WinDbg のみ)File | を使用します。 [[最近使ったファイル](file---recent-files.md)] コマンドを使用して、WinDbg で最近開いた4つのソースファイルのいずれかを開きます。

-   (WinDbg のみ)File | を使用します。 [現在のウィンドウ](file---close-current-window.md)コマンドを閉じるか、[ソースウィンドウ](source-window.md)の隅にある **[閉じる]** ボタンをクリックして、ソースファイルを閉じます。

ソースファイルの使用方法の詳細については、「[ソースモードでのデバッグ](debugging-in-source-mode.md)」を参照してください。

 

 





