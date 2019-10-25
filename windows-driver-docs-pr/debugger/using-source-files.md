---
title: ソース ファイルの使用
description: ソース ファイルの使用
ms.assetid: c6dfcb37-140f-43d8-aa15-14f0317b5e19
keywords:
- デバッガーエンジン API、ソース
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f7c1622b1ca49e43886db78bd7d990448686afd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838803"
---
# <a name="using-source-files"></a>ソース ファイルの使用


[デバッガーエンジン](introduction.md#debugger-engine)は、*ソースパス*を保持します。これは、現在のターゲットに関連付けられているソースコードファイルを含むディレクトリとソースサーバーの一覧です。 デバッガーエンジンは、これらのディレクトリとソースサーバーでソースファイルを検索できます。 シンボルファイルを使用すると、デバッガーエンジンはソースファイルの行とターゲットのメモリ内の場所を一致させることができます。

デバッガーでソースファイルを使用する方法の概要については、「[ソースモードでのデバッグ](debugging-in-source-mode.md)」を参照してください。 ソースパスの概要については、「[ソースパス](source-path.md)」を参照してください。 デバッガーエンジンでのソースサーバーの使用の概要については、「[ソースサーバーの使用](using-a-source-server.md)」を参照してください。

### <a name="span-idsource_pathspanspan-idsource_pathspansource-path"></a><span id="source_path"></span><span id="SOURCE_PATH"></span>ソースパス

ソースパスにディレクトリまたはソースサーバーを追加するには、 [**Appendsourcepath**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-appendsourcepath)メソッドを使用します。 ソースパス全体は[**getsourcepath**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getsourcepath)によって返され、 [**setsourcepath**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-setsourcepath)を使用して変更できます。 1つのディレクトリまたはソースサーバーは、 [**Getsourcepathelement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getsourcepathelement)を使用してソースパスから取得できます。

ソースパスを基準とするソースファイルを検索するには、 [**findsourcefile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-findsourcefile)またはを使用します。移行元サーバーを使用する場合の詳細なオプションについては、 [**Findsourcefileandtoken**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugadvanced3-findsourcefileandtoken)を使用します。 **Findsourcefileandtoken**は、 [**Getsourcefileinformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugadvanced3-getsourcefileinformation)と共に使用して、移行元サーバー上のファイルに関連する変数を取得することもできます。

### <a name="span-idmatching_source_files_to_code_in_memoryspanspan-idmatching_source_files_to_code_in_memoryspanmatching-source-files-to-code-in-memory"></a><span id="matching_source_files_to_code_in_memory"></span><span id="MATCHING_SOURCE_FILES_TO_CODE_IN_MEMORY"></span>ソースファイルとメモリ内のコードの一致

デバッガーエンジンには、ソースファイル内の行に対応するメモリ位置を検索するための3つのメソッドが用意されています。 1行のソースコードをメモリ位置にマップするには、 [**GetOffsetByLine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getoffsetbyline)を使用します。 複数のソース行または近くのソース行のメモリ位置を検索するには、 [**GetSourceEntriesByLine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getsourceentriesbyline)を使用します。 [**GetSourceFileLineOffsets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getsourcefilelineoffsets)メソッドは、ソースファイル内のすべての行のメモリ位置を返します。

逆の操作を実行し、ターゲットのメモリ内の場所に一致するソースファイルの行を検索するには、 [**Getlinebyoffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getlinebyoffset)を使用します。

ソースファイル内のメモリの場所と行の関係は必ずしも1対1ではない**ことに注意**してください  。 1行のソースコードが複数のメモリ位置に対応し、1つのメモリ位置がソースコードの複数行に対応する可能性があります。

 

 

 





