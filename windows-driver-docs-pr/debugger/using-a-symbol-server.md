---
title: シンボル サーバーの使用
description: シンボル サーバーの使用
ms.assetid: 6c1687c7-7b9d-45f7-8778-c7284c4a8222
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ab2d732ed51664ffa7065968f79821ad7cd1990
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527796"
---
# <a name="using-a-symbol-server"></a>シンボル サーバーの使用


デバッガー シンボルから正しいシンボル ファイルを自動的に取得する製品の名前を知る必要なく、ユーザーのシンボル ファイルのインデックス付きコレクション - を格納するシンボル サーバーの有効では、リリース、またはビルド番号。 Windows のツールをデバッグ パッケージには、シンボル サーバーが含まれています。 [SymSrv](symsrv.md) (symsrv.exe)。

### <a name="span-idusingsymsrvwithadebuggerspanspan-idusingsymsrvwithadebuggerspanusing-symsrv-with-a-debugger"></a><span id="using_symsrv_with_a_debugger"></span><span id="USING_SYMSRV_WITH_A_DEBUGGER"></span>デバッガーで SymSrv の使用

SymSrv は、WinDbg、KD、NTSD、または CDB で使用できます。

デバッガーでこのシンボル サーバーを使用するテキストを単に含める**srv\\*** シンボル パスにします。 次に、例を示します。

```console
set _NT_SYMBOL_PATH = srv*DownstreamStore*SymbolStoreLocation
```

場所*DownstreamStore*ローカル ディレクトリまたは個々 のシンボルのファイルをキャッシュに使用されるネットワーク共有を指定します、 *SymbolStoreLocation*シンボル ストアの場所をフォームのいずれかです *\\ \\server\\共有*またはインターネット アドレス。 詳しい構文オプションについて、次を参照してください。 [SymSrv 使用の高度な](advanced-symsrv-use.md)します。

マイクロソフトでは、Windows シンボルをパブリックに使用できるようにする Web サイトがあります。 次のように、シンボル パスにこのサイトを直接参照できます。

```console
set _NT_SYMBOL_PATH=srv*DownstreamStore*https://msdl.microsoft.com/download/symbols
```

もう一度、 *DownstreamStore*個々 のシンボル ファイルをキャッシュに使用されるローカル ディレクトリまたはネットワーク共有を指定します。 詳細については、次を参照してください。 [Microsoft パブリック シンボル](microsoft-public-symbols.md)します。

シンボル ストアを作成する場合は、web (HTTP) へのアクセスのシンボル ストアの構成を参照してください、または独自のシンボル サーバーまたはシンボル ストアに書き込む[シンボル ストアとシンボル サーバー](symbol-stores-and-symbol-servers.md)します。

### <a name="span-idusingagestoretoreducethecachesizespanspan-idusingagestoretoreducethecachesizespanusing-agestore-to-reduce-the-cache-size"></a><span id="using_agestore_to_reduce_the_cache_size"></span><span id="USING_AGESTORE_TO_REDUCE_THE_CACHE_SIZE"></span>AgeStore を使用して、キャッシュのサイズを小さくには

デバッグ セッションが完了したら、SymSrv によってダウンロードされたすべてのシンボル ファイルは、ハード ドライブに残ります。 シンボル キャッシュのサイズを制御するには、指定した日付よりも古いキャッシュ ファイルを削除するかを指定したサイズ以下のキャッシュの内容を減らす、AgeStore ツールを使用できます。 詳細については、次を参照してください。 [AgeStore](agestore.md)します。

 

 





