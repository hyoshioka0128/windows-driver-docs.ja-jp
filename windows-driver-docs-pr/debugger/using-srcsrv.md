---
title: SrcSrv の使用
description: SrcSrv の使用
ms.assetid: 2696e5e9-343f-49a2-bdab-23a54f8c9e5c
keywords:
- ソースサーバー、SrcSrv (srcsrv .dll)
- SrcSrv, 概要
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41f5f13dd8d613e427191eba775256a11e2bc6cb
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534749"
---
# <a name="using-srcsrv"></a>SrcSrv の使用


WinDbg、KD、NTSD、または CDB で[Srcsrv](srcsrv.md)を使用するには、最新バージョンの[Windows パッケージ用デバッグツール](https://docs.microsoft.com/windows-hardware/drivers/debugger/)(バージョン6.3 以降) がインストールされていることを確認します。 次に、ソースパスにあるテキストを、 `srv*` ソースパスにも含まれているディレクトリからセミコロンで区切って入力します。

次に例を示します。

```dbgcmd
.srcpath srv*;c:\someSourceCode
```

ソースパスが前の例のように設定されている場合、デバッガーは最初に[Srcsrv](srcsrv.md)を使用して、ターゲットモジュールのシンボルファイルに指定されている場所からソースファイルを取得します。 SrcSrv がソースファイルを取得できない場合、デバッガーは c: soを使ってファイルを取得しようとし \\ ます。 Srv がパス内の最初の要素であるか、 \* 後で表示されるかにかかわらず、デバッガーは、パスに示されている他のディレクトリを検索する前に、常に SymSrv を使用します。

ソースファイルが[Srcsrv](srcsrv.md)によって取得された場合、デバッグセッションが終了した後も、ハードドライブに残ります。 ソースファイルは、ローカルのホームディレクトリの src サブディレクトリに格納されます (シンボルサーバーとは異なり、ソースサーバーは構文自体でローカルキャッシュを指定しません `srv*` )。 ホームディレクトリは、Windows のインストールディレクトリのデバッグツールに既定で設定されています。これは、 [**! homedir**](-homedir.md)拡張機能を使用するか、dbghelp homedir 環境変数を設定することによって変更でき \_ ます。 ホームディレクトリの src サブディレクトリが存在しない場合は、作成されます。

### <a name="span-iddebugging_srcsrvspanspan-iddebugging_srcsrvspandebugging-srcsrv"></a><span id="debugging_srcsrv"></span><span id="DEBUGGING_SRCSRV"></span>SrcSrv のデバッグ

デバッガーからソースファイルを抽出するときに問題が発生した場合は、-n コマンドラインパラメーターを指定してデバッガーを起動し、実際のソース抽出コマンドと、それらのコマンドの出力を表示します。 ! Sym が雑音のコマンドでも同じことが行われますが、以前の抽出の試行から重要な情報が既に失われている可能性があります。 これは、デバッガーが、到達できないと思われるバージョン管理リポジトリからソースにアクセスしようとするためです。

### <a name="span-idretrieving_source_filesspanspan-idretrieving_source_filesspanretrieving-source-files"></a><span id="retrieving_source_files"></span><span id="RETRIEVING_SOURCE_FILES"></span>ソースファイルの取得

[**. Open (オープンソースファイル)**](-open--open-source-file-.md)コマンドを使用して、 [srcsrv](srcsrv.md)経由で新しいソースファイルを開く場合は、-m Address パラメーターを含める必要があります。

前に示したデバッガー以外のツールから[srcsrv](srcsrv.md)の使用を容易にするために、DBGHELP API は**symgetsourcefile**関数を介して srcsrv 機能にアクセスできるようにします。 取得するソースファイルの名前を取得するには、 **SymEnumSourceFiles**関数または**SymGetLineFromAddr64**関数を呼び出します。 DbgHelp API の詳細については、dbghelp .chm のドキュメントを参照してください。このドキュメントは、デバッグツールの Windows インストールディレクトリの sdk/help サブディレクトリにあります。または、[デバッグヘルプライブラリ](https://docs.microsoft.com/windows/win32/debug/debug-help-library)を参照してください。

### <a name="span-idusing_agestore_to_reduce_the_cache_sizespanspan-idusing_agestore_to_reduce_the_cache_sizespanusing-agestore-to-reduce-the-cache-size"></a><span id="using_agestore_to_reduce_the_cache_size"></span><span id="USING_AGESTORE_TO_REDUCE_THE_CACHE_SIZE"></span>AgeStore を使用してキャッシュサイズを小さくする

デバッグセッションが終了すると、 [Srcsrv](srcsrv.md)によってダウンロードされたソースファイルは、ハードドライブに残ります。 ソースキャッシュのサイズを制御するには、AgeStore ツールを使用して、指定した日付よりも古いキャッシュファイルを削除するか、キャッシュの内容を指定されたサイズより小さくすることができます。 詳細については、「 [Agestore](agestore.md)」を参照してください。

 

 





