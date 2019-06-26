---
title: ソース ファイルの使用
description: ソース ファイルの使用
ms.assetid: c6dfcb37-140f-43d8-aa15-14f0317b5e19
keywords:
- エンジンの API のデバッガー、ソース
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: d8452c5881edb3c171b5f7a8c4a736a2d80cd36f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368610"
---
# <a name="using-source-files"></a>ソース ファイルの使用


[デバッガー エンジン](introduction.md#debugger-engine)保持、*ソース パス*ディレクトリと現在のターゲットに関連付けられているソース コード ファイルが含まれている移行元サーバーの一覧します。 デバッガー エンジンには、これらのディレクトリとソース ファイルをソース サーバーを検索できます。 シンボル ファイルを利用して、デバッガー エンジンは、ターゲットのメモリ内の場所でソース ファイル内の行を照合できます。

デバッガーでソース ファイルの使用の概要については、次を参照してください。[元のモードでデバッグ](debugging-in-source-mode.md)します。 ソース パスの概要については、次を参照してください。[ソース パス](source-path.md)します。 デバッガー エンジンからの移行元サーバーを使用しての概要については、次を参照してください。[移行元サーバーを使用して](using-a-source-server.md)します。

### <a name="span-idsourcepathspanspan-idsourcepathspansource-path"></a><span id="source_path"></span><span id="SOURCE_PATH"></span>ソース パス

ソース パスには、ディレクトリまたはソース サーバーを追加するには、メソッドを使用して[ **AppendSourcePath**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-appendsourcepath)します。 全体のソース パスは、によって返される[ **GetSourcePath** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-getsourcepath)を使用して変更できる[ **SetSourcePath**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-setsourcepath)します。 ソース パスを使用して 1 つのディレクトリまたはソース サーバーを取得できる[ **GetSourcePathElement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-getsourcepathelement)します。

ソース パスを基準とソース ファイルを検索するには使用[ **FindSourceFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-findsourcefile)または、移行元サーバーを使用する場合の高度なオプションは、使用[ **FindSourceFileAndToken**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugadvanced3-findsourcefileandtoken). **FindSourceFileAndToken**とともに使用することができますも[ **GetSourceFileInformation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugadvanced3-getsourcefileinformation)をソース サーバー上のファイルに関連する変数を取得します。

### <a name="span-idmatchingsourcefilestocodeinmemoryspanspan-idmatchingsourcefilestocodeinmemoryspanmatching-source-files-to-code-in-memory"></a><span id="matching_source_files_to_code_in_memory"></span><span id="MATCHING_SOURCE_FILES_TO_CODE_IN_MEMORY"></span>メモリ内のコードに一致するソース ファイル

デバッガー エンジンは、ソース ファイル内の行に対応するメモリ位置を検索するための 3 つのメソッドを提供します。 ソース コードの 1 つの行をメモリ位置をマップするには使用[ **GetOffsetByLine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-getoffsetbyline)します。 1 つ以上のソース行、またはソースの近くにある行のメモリ位置を検索するを使用して、 [ **GetSourceEntriesByLine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-getsourceentriesbyline)します。 [ **GetSourceFileLineOffsets** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-getsourcefilelineoffsets)メソッドは、ソース ファイル内のすべての行のメモリ位置を返します。

逆の操作を実行し、ターゲットのメモリ内の場所に一致するソース ファイルの行を見つけて使用[ **GetLineByOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-getlinebyoffset)します。

**注**  メモリの場所とソース ファイル内の行の間のリレーションシップが必ずしも 1 対 1 ではありません。 複数のメモリ位置に対応するソース コードの 1 行の場合、複数のソース コード行に対応する 1 つのメモリ位置のことができます。

 

 

 





