---
title: ソース パス
description: このトピックでは、個々 のソース ファイルを読み込んだりするソース パスを設定する方法について説明します。
ms.assetid: b5dcb557-b413-401a-be4b-2d45b2597e6c
keywords: ソース ファイルとパス、ソース パス
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 686870221ff72a5ecf60cd8a56c18c32bf97302d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537656"
---
# <a name="source-path"></a>ソース パス


## <span id="ddk_source_path_dbg"></span><span id="DDK_SOURCE_PATH_DBG"></span>


*ソース パス*C および C++ ソース ファイルが配置されるディレクトリを指定します。

実行可能ファイルが作成されたコンピューター上のユーザー モード プロセスをデバッグしている場合と、ソース ファイルは、元の場所にまだの場合は、デバッガーがソース ファイルを自動的に検索します。

他のほとんどの状況では、ソース パスを設定または個々 のソース ファイルを読み込むことがあります。

実行する際[デバッガーからのリモート デバッグ](remote-debugging-through-the-debugger.md)、デバッグのサーバーには、ソース パスが使用されます。 WinDbg デバッガーとしてを使用している場合は、各デバッグ クライアントもには、独自*ローカル ソース パス*します。 すべてのソースに関連するコマンドは、ローカル コンピューターのソース ファイルにアクセスします。 任意のクライアントまたはソースのコマンドを使用するサーバー上の適切なパスを設定する必要があります。

この複数のパスのシステムでは、実際には、他のクライアントまたはサーバーとソース ファイルを共有することがなくソースに関連するコマンドを使用するデバッグ クライアントもできます。 このシステムは秘密がある場合に役立ちます。 または、機密ソース ファイル、ユーザーの 1 つがへのアクセス。

ソース パスに関係なく、いつでも、ソース ファイルを読み込むこともできます。

### <a name="span-idsourcepathsyntaxspanspan-idsourcepathsyntaxspansource-path-syntax"></a><span id="source_path_syntax"></span><span id="SOURCE_PATH_SYNTAX"></span>ソース パスの構文

デバッガーのソース パスは、セミコロンで区切られた複数のディレクトリ パスで構成される文字列です。

相対パスがサポートされています。 ただし、常に同じディレクトリから、デバッガーを起動する場合を除きする必要がありますを追加するドライブ文字またはネットワークの各パスの前に共有します。 ネットワーク共有もサポートされます。

**注**ソース サーバーを使用するソース ファイルにアクセスする最も効率的な方法は、企業ネットワークに接続している場合。 使用して、移行元サーバーを使用することができます、 **srv\\***、ソース パス内の文字列。 移行元サーバーの詳細については、次を参照してください。[移行元サーバーを使用して](using-a-source-server.md)します。

 

### <a name="span-idcontrollingthesourcepathspanspan-idcontrollingthesourcepathspancontrolling-the-source-path"></a><span id="controlling_the_source_path"></span><span id="CONTROLLING_THE_SOURCE_PATH"></span>ソース パスを制御します。

ソース パスとローカルのソース パスを制御するには、次のいずれかの操作を行います。

-   使用して、デバッガーを開始する前に、 \_NT\_ソース\_パス[環境変数](environment-variables.md)ソース パスを設定します。 この環境変数を介して無効なディレクトリを追加しようとすると、デバッガーは、このディレクトリを無視します。

-   デバッガーを起動するときに使用して、 **- srcpath**[コマンド ライン オプション](command-line-options.md)ソース パスを設定します。

-   使用して、 [ **.srcpath (ソース パスの設定)** ](-srcpath---lsrcpath--set-source-path-.md)コマンドを表示、設定、変更、またはソース パスに追加します。 移行元サーバーを使用している場合[ **.srcfix (ソース サーバーを使用)** ](-srcfix---lsrcfix--use-source-server-.md)多少簡単になります。

-   (WinDbg のみ)使用して、 [ **.lsrcpath (ローカル ソース パスを設定する)** ](-srcpath---lsrcpath--set-source-path-.md)コマンドを表示、設定、変更、またはローカル ソース パスに追加します。 移行元サーバーを使用している場合[ **.lsrcfix (ローカル ソース サーバーを使用する)** ](-srcfix---lsrcfix--use-source-server-.md)多少簡単になります。 パラメーター lscrpath とコマンド ライン WinDbg を使用することもできます。 詳細については、次を参照してください。 [ **WinDbg コマンド ライン オプション**](windbg-command-line-options.md)します。

-   (WinDbg のみ)使用して、[ファイル |ソース ファイル パス](file---source-file-path.md)コマンドまたは表示するには CTRL + P キーを押して設定、変更、またはソース パスまたはローカル ソース パスを追加します。

開くも直接または、次のいずれかの方法とソース ファイルを閉じることがことができます。

-   使用して、 [ **(ロードまたはアンロード ソース ファイル) の lsf** ](lsf--lsf---load-or-unload-source-file-.md)を開くか、ソース ファイルを閉じるコマンド。

-   (WinDbg のみ)使用して、 [ **.open (ソース ファイルを開く)** ](-open--open-source-file-.md)コマンド ソース ファイルを開きます。

-   (WinDbg のみ)使用して、[ファイル | オープン ソース ファイル](file---open-source-file.md)コマンドまたは ctrl キーを押しながら o ソース ファイルを開きます。 使用することも、**オープン ソース ファイル (ctrl + o)** ボタン (![オープン ソース ファイル ボタンのスクリーン ショット](images/tbopen.png)) ツールバー。

    **注**  を使用すると**ファイル |ソース ファイルを開く**(またはショートカット メニューまたはボタン同等のもの) にソース ファイルを開くには、そのファイルのパスが自動的にソース パスに追加します。

     

-   (WinDbg のみ)使用して、[ファイル |最近使ったファイル](file---recent-files.md)WinDbg で最近開いたいる 4 つのソース ファイルのいずれかを開くコマンド。

-   (WinDbg のみ)使用して、[ファイル |現在のウィンドウを閉じます](file---close-current-window.md)コマンドまたはをクリックして、**閉じます**の隅にあるボタン、[ソース ウィンドウ](source-window.md)ソース ファイルを閉じます。

ソース ファイルを使用する方法の詳細については、次を参照してください。[元のモードでデバッグ](debugging-in-source-mode.md)します。

 

 





