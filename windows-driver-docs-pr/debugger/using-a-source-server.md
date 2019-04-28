---
title: ソース サーバーの使用
description: ソース サーバーの使用
ms.assetid: b3467f26-1ce3-42cb-a8c8-a7d10efc5079
keywords:
- 移行元サーバー (srcsrv.dll)
- 移行元サーバー (srcsrv.dll), 概要
- SrcSrv (srcsrv.dll)
- SrcSrv (srcsrv.dll), 概要
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e2cf4d155227156e6f98ead371ffe6df53acb32
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367962"
---
# <a name="using-a-source-server"></a>ソース サーバーの使用


移行元サーバーでは、現在のターゲットに一致するソース ファイルを自動的に取得するデバッガーを使用できます。 移行元サーバーを使用するには、は、ソースのビルド時にインデックスが作成されているし、あるソース ファイルの場所は PDB ファイルに埋め込まれているバイナリをデバッグする必要があります。

移行元サーバーを含むデバッグ ツールの Windows [SrcSrv](srcsrv.md) (Srcsrv.exe)。

### <a name="span-idusingsrcsrvwithadebuggerspanspan-idusingsrcsrvwithadebuggerspanusing-srcsrv-with-a-debugger"></a><span id="using_srcsrv_with_a_debugger"></span><span id="USING_SRCSRV_WITH_A_DEBUGGER"></span>デバッガーで SrcSrv の使用

[SrcSrv](srcsrv.md) WinDbg、KD、NTSD、または CDB で使用できます。

使用する[SrcSrv](srcsrv.md)デバッガー、srv にソース パスを設定するには、次のコマンドを入力します。\*します。

```dbgcmd
.srcfix
```

次のコマンドを入力して、同じ結果を得ることができます。

```dbgcmd
.srcpath srv*
```

ソース パスを srv 設定\*対象モジュールのシンボル ファイルで指定された場所からソース ファイルを取得することをデバッガーに指示します。

使用する場合[SrcSrv](srcsrv.md)とも、ソース パスにディレクトリの一覧を含む、セミコロンで区切る`srv*`パスに含まれるすべてのディレクトリから。

以下に例を示します。

```dbgcmd
.srcpath srv*;c:\someSourceCode 
```

ソース パスは、前の例で示すように設定されている場合、デバッガーは最初は[SrcSrv](srcsrv.md)対象モジュールのシンボル ファイルで指定された場所からソース ファイルを取得します。 デバッガーが c: から取得しようとした SrcSrv がソース ファイルを取得できない場合は、\\someSourceCode します。 かどうかに関係なく srv\*パスの最初の要素または後に表示されるため、デバッガーは、パスに表示されているその他のディレクトリを検索する前に常に SymSrv を使用します。

使用することも[ **.srcfix +** ](-srcfix---lsrcfix--use-source-server-.md)を追加する`srv*`に次の例で示すように、既存のソース パスにします。

```dbgcmd
3: kd> .srcpath c:\mySource
Source search path is: c:\mySource
3: kd> .srcfix+
Source search path is: c:\mySource;SRV*
```

移行元サーバーによってソース ファイルを取得すると場合、は、デバッグ セッションが完了したら、ハード ドライブに残ります。 ホーム ディレクトリの src サブディレクトリでソース ファイルがローカルに保存 (、シンボル サーバーとは異なり、移行元サーバーは指定のローカル キャッシュ、`srv*`の構文そのもの)。 ホーム ディレクトリの既定値は、デバッガーのインストール ディレクトリ。使用して変更すること、 [ **! homedir** ](-homedir.md)拡張機能を設定、DBGHELP\_HOMEDIR 環境変数。 このサブディレクトリが存在しない場合は、それが作成されます。

使用する場合、 [ **.open (ソース ファイルを開く)** ](-open--open-source-file-.md)を通じて新しいソース ファイルを開くコマンド[SrcSrv](srcsrv.md)、-m アドレス パラメーターを含める必要があります。

詳しくは、ソースのインデックスまたは独自ソース管理プロバイダー モジュールを作成する場合に表示する方法の[SrcSrv](srcsrv.md)します。

### <a name="span-idusingagestoretoreducethecachesizespanspan-idusingagestoretoreducethecachesizespanusing-agestore-to-reduce-the-cache-size"></a><span id="using_agestore_to_reduce_the_cache_size"></span><span id="USING_AGESTORE_TO_REDUCE_THE_CACHE_SIZE"></span>AgeStore を使用して、キャッシュのサイズを小さくには

ソースによってダウンロードされたファイル[SrcSrv](srcsrv.md)デバッグ セッションが完了したら、ハード ドライブに残ります。 ソースのキャッシュのサイズを制御するには、指定した日付よりも古いキャッシュ ファイルを削除するかを指定したサイズ以下のキャッシュの内容を減らす、AgeStore ツールを使用できます。 詳細については、次を参照してください。 [AgeStore](agestore.md)します。

 

 





