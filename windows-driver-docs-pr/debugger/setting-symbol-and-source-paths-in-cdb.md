---
title: CDB でシンボルと実行可能イメージのパスを設定します。
description: CDB でシンボルと実行可能イメージのパスを設定します。
ms.assetid: 6BBB7DC4-716E-4717-8C48-7E778907E85B
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9887d3e9dd7c97199ef2572b098311c7a9ef47ec
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552497"
---
# <a name="setting-symbol-and-executable-image-paths-in-cdb"></a>CDB でシンボルと実行可能イメージのパスを設定します。


## <a name="span-idddksymbolpathdbgspanspan-idddksymbolpathdbgspansymbol-path"></a><span id="ddk_symbol_path_dbg"></span><span id="DDK_SYMBOL_PATH_DBG"></span>シンボル パス


シンボル パスは、シンボル ファイルが配置されるディレクトリを指定します。 シンボルとシンボル ファイルの詳細については、[シンボル](symbols.md)を参照してください。

**注**  シンボル サーバーを使用するアクセスのシンボルを最も効率的な方法は、インターネットまたは企業ネットワークに接続している場合。 シンボル サーバーを使用するには、srv を使用して\*または symsrv\*シンボル パス内の文字列。 シンボル サーバーの詳細については、[シンボル ストアとシンボル サーバー](symbol-stores-and-symbol-servers.md)を参照してください。

 

CDB でシンボル パスを制御するには、次のいずれかの操作を行います。

-   入力、 [ **.sympath (シンボル パスの設定)** ](-sympath--set-symbol-path-.md)コマンド。 シンボル サーバーを使用している場合、 [ **.symfix (シンボル ストア パスの設定)** ](-symfix--set-symbol-store-path-.md)コマンドは、.sympath に似ていますが、入力を省略できます。

-   デバッガーを起動するときに使用して、 **-y**コマンド ライン オプション。 参照してください[ **CDB コマンド ライン オプション**](cdb-command-line-options.md)します。

-   使用して、デバッガーを開始する前に、 \_NT\_シンボル\_パスと\_NT\_ALT\_シンボル\_パス[環境変数](environment-variables.md)を設定するにはパス。 シンボル パスが追加することによって作成された\_NT\_シンボル\_後パス\_NT\_ALT\_シンボル\_パス。 (通常は、パスがによって設定されます、 \_NT\_シンボル\_パス。 使用するただし、 \_NT\_ALT\_シンボル\_共有シンボル ファイルのプライベート バージョンがある場合など、特殊なケースでこれらの設定を上書きするパス)。

    **注**  を使用する場合、 **-sins**コマンド ライン オプション、デバッガーがシンボルの path 環境変数を無視します。

     

## <a name="span-idexecutableimagepathspanspan-idexecutableimagepathspanspan-idexecutableimagepathspanexecutable-image-path"></a><span id="Executable_Image_Path"></span><span id="executable_image_path"></span><span id="EXECUTABLE_IMAGE_PATH"></span>実行可能イメージのパス


### <span id="ddk_executable_image_path_dbg"></span><span id="DDK_EXECUTABLE_IMAGE_PATH_DBG"></span>

実行可能ファイルとは、プロセッサが実行できるバイナリ ファイルです。 これらのファイルには、通常、.exe、.dll、または .sys ファイル名拡張子があります。 実行可能ファイルは、特に大規模なアプリケーションの単位として実行可能ファイルが説明されている場合、モジュールとも呼ばれます。 Windows オペレーティング システムが実行可能ファイルを実行する前にメモリに読み込みます。 実行可能イメージまたはイメージは、メモリ内で実行可能ファイルのコピーが呼び出されます。

**注**  これらの用語が不正確に使用される場合があります。 たとえば、いくつかのドキュメントでは、ディスク上の実際のファイルの「イメージ」を使用する可能性があります。 また、Windows カーネルと HAL 特殊なモジュール名であります。 たとえば、 **nt** Ntoskrnl.exe ファイルに対応するモジュール。

 

実行可能イメージのパスは、バイナリ実行可能ファイルに存在するディレクトリを指定します。

ほとんどの場合、デバッガーは、このファイルのパスを設定する必要はありませんので実行可能ファイルのファイルの場所を認識します。

ただし、このパスが必要な場合があります。 たとえば、カーネル モード[小さいメモリ ダンプ](small-memory-dump.md)ファイルにすべての停止エラー (つまり、クラッシュ) 時にメモリに存在する実行可能ファイルがあらかじめ含まれていない操作を行います。 同様に、ユーザー モードのミニダンプ ファイルには、アプリケーション バイナリはありません。 実行可能ファイルのパスを設定した場合、デバッガーはこれらのバイナリ ファイルを検索できます。

デバッガーの実行可能イメージのパスは、セミコロンで区切られた複数のディレクトリ パスで構成される文字列です。 相対パスがサポートされています。 ただし、常に同じディレクトリから、デバッガーを起動する場合を除きする必要がありますを追加するドライブ文字またはネットワークの各パスの前に共有します。 ネットワーク共有もサポートされます。 デバッガーは、実行可能イメージのパスに再帰的に検索します。 デバッガーは、このパスに表示されている各ディレクトリのサブディレクトリを検索します。

CDB で実行可能イメージのパスを制御するには、次のいずれかの操作を行います。

-   入力、 [ **.exepath (実行可能ファイル パスの設定)** ](-exepath--set-executable-path-.md)コマンド。

-   デバッガーを起動するときに使用して、 **-i**コマンド ライン オプション。 参照してください[ **CDB コマンド ライン オプション**](cdb-command-line-options.md)します。

-   使用して、デバッガーを開始する前に、 \_NT\_実行可能ファイル\_イメージ\_パス[環境変数](environment-variables.md)パスを設定します。

    **注**  を使用する場合、 **-sins**コマンド ライン オプション、デバッガーには、実行可能イメージの path 環境変数が無視されます。

     

 

 





