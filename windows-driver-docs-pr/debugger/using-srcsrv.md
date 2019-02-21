---
title: SrcSrv の使用
description: SrcSrv の使用
ms.assetid: 2696e5e9-343f-49a2-bdab-23a54f8c9e5c
keywords:
- ソース サーバー、SrcSrv (srcsrv.dll)
- SrcSrv, 概要
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 650872e6dfb0ef7d1f7ac0c1d27050ec985255a7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531321"
---
# <a name="using-srcsrv"></a>SrcSrv の使用


使用する[SrcSrv](srcsrv.md) WinDbg、KD、NTSD、または CDB での最新のバージョンがインストールされていることを確認、[ツールを Windows のデバッグ](https://docs.microsoft.com/windows-hardware/drivers/debugger/)パッケージ (バージョン 6.3 またはそれ以降)。 次に、テキストを含めます`srv*`ソース パス内にあるすべてのディレクトリからのセミコロンで区切られた、ソース パスにします。

次に、例を示します。

```dbgcmd
.srcpath srv*;c:\someSourceCode
```

ソース パスは、前の例で示すように設定されている場合、デバッガーは最初は[SrcSrv](srcsrv.md)対象モジュールのシンボル ファイルで指定された場所からソース ファイルを取得します。 デバッガーが c: から取得しようとした SrcSrv がソース ファイルを取得できない場合は、\\someSourceCode します。 かどうかに関係なく srv\*パスの最初の要素または後に表示されるため、デバッガーは、パスに表示されているその他のディレクトリを検索する前に常に SymSrv を使用します。

場合によっては、ソース ファイルを取得してください。 [SrcSrv](srcsrv.md)、デバッグ セッションが完了したら、ハード ドライブに残ります。 ホーム ディレクトリの src サブディレクトリでソース ファイルがローカルに保存 (、シンボル サーバーとは異なり、移行元サーバーは指定のローカル キャッシュ、`srv*`の構文そのもの)。 Windows のツールのデバッグのインストール ディレクトリにホーム ディレクトリの既定値使用して変更すること、 [ **! homedir** ](-homedir.md)拡張機能を設定、DBGHELP\_HOMEDIR 環境変数。 ホーム ディレクトリの src サブディレクトリが存在しない場合は作成されます。

### <a name="span-iddebuggingsrcsrvspanspan-iddebuggingsrcsrvspandebugging-srcsrv"></a><span id="debugging_srcsrv"></span><span id="DEBUGGING_SRCSRV"></span>SrcSrv のデバッグ

デバッガーからソース ファイルを抽出します。 問題が発生した場合は、実際のソース抽出コマンドと共にそれらのコマンドの出力を表示する-n コマンド ライン パラメーターを使用してデバッガーを起動します。 ! Sym ノイズの多いコマンドは同じですが、既に不足している前回の抽出から重要な情報。 デバッガーは到達できない表示されるバージョン管理リポジトリからソースにアクセスしようとしているためにです。

### <a name="span-idretrievingsourcefilesspanspan-idretrievingsourcefilesspanretrieving-source-files"></a><span id="retrieving_source_files"></span><span id="RETRIEVING_SOURCE_FILES"></span>ソース ファイルを取得します。

使用する場合、 [ **.open (ソース ファイルを開く)** ](-open--open-source-file-.md)を通じて新しいソース ファイルを開くコマンド[SrcSrv](srcsrv.md)、-m アドレス パラメーターを含める必要があります。

使用を容易に[SrcSrv](srcsrv.md) DbgHelp API がを通じて SrcSrv 機能へのアクセスを提供する前の表に、デバッガー以外のツールから、 **SymGetSourceFile**関数。 取得するソース ファイルの名前を取得する、 **SymEnumSourceFiles**または**SymGetLineFromAddr64**関数。 DbgHelp API の詳細については、ドキュメントを参照して、dbghelp.chm、ツールを Windows のデバッグのインストール ディレクトリの sdk のヘルプ/サブディレクトリで見つかりますが、またはを参照してください[デバッグ ヘルプ ライブラリ](https://go.microsoft.com/fwlink/p/?linkid=125231)します。

### <a name="span-idusingagestoretoreducethecachesizespanspan-idusingagestoretoreducethecachesizespanusing-agestore-to-reduce-the-cache-size"></a><span id="using_agestore_to_reduce_the_cache_size"></span><span id="USING_AGESTORE_TO_REDUCE_THE_CACHE_SIZE"></span>AgeStore を使用して、キャッシュのサイズを小さくには

ソースによってダウンロードされたファイル[SrcSrv](srcsrv.md)デバッグ セッションが完了したら、ハード ドライブ上に残ります。 ソースのキャッシュのサイズを制御するには、指定した日付より古いキャッシュ ファイルを削除するかを指定したサイズ以下のキャッシュの内容を減らす AgeStore ツールが使用できます。 詳細については、次を参照してください。 [AgeStore](agestore.md)します。

 

 





