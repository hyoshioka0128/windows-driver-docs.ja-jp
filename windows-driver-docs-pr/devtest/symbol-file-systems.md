---
title: シンボル ファイル システム
description: シンボル ファイル システム
ms.assetid: 06f536e2-13d8-4727-9d34-a29a63eb01bc
keywords:
- BinPlace WDK、シンボル ファイル システム
- シンボル ファイル WDK BinPlace
- 現在のシンボル ファイル システム WDK BinPlace
- 古いシンボル ファイル システム WDK
- .pdf ファイル
- ファイルの WDK BinPlace を pdf のシンボル
- ファイルの WDK BinPlace を dbg シンボル
- .dbg ファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e2b789cb4f24ec4c92817348b5dcd591ae5927c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362176"
---
# <a name="symbol-file-systems"></a>シンボル ファイル システム


## <span id="ddk_symbol_file_systems_tools"></span><span id="DDK_SYMBOL_FILE_SYSTEMS_TOOLS"></span>


2 つの一般的なシンボル ファイル システムがあります。 このドキュメントでは、これらが参照されますとして、*現在のシステム*と*古いシステム*します。

### <a name="span-idcurrentsymbolfilesystemspanspan-idcurrentsymbolfilesystemspancurrent-symbol-file-system"></a><span id="current_symbol_file_system"></span><span id="CURRENT_SYMBOL_FILE_SYSTEM"></span>現在のシンボル ファイル システム

現在のシステムでは常に 2 つのファイル: 実行可能ファイルと .pdb ファイル。 .Pdb ファイルには、すべてのシンボルが含まれています。 実行可能ファイルには、.pdb ファイルへのポインターが含まれています。

.Pdb シンボル ファイルにプライベート シンボルが含まれている場合、BinPlace は out には、この情報を削除し、削除されたシンボル ファイルを生成できます。 参照してください[パブリック シンボルとプライベート シンボルの](public-symbols-and-private-symbols.md)詳細についてはします。

### <a name="span-idoldsymbolfilesystemspanspan-idoldsymbolfilesystemspanold-symbol-file-system"></a><span id="old_symbol_file_system"></span><span id="OLD_SYMBOL_FILE_SYSTEM"></span>古いシンボル ファイル システム

古いシステムでは、実行可能ファイルとシンボル ファイル 2 つの方法で整列することができます。

-   実行可能ファイルと .pdb ファイル。 これにより、ほとんどのシンボル情報は、.pdb ファイルです。 シンボル情報の残りの部分は、実行可能ファイルに含まれます。 実行可能ファイルには、.pdb ファイルへのポインターも含まれています。

-   実行可能ファイル、.pdb ファイル、および .dbg ファイル。 .Pdb ファイルは、2 つのファイルの配置と同じ: シンボルのほとんどを保持します。 .Dbg ファイル、シンボル情報の残りの部分にあります。 実行可能ファイルにシンボル情報がありません。 実行可能ファイルは、.dbg ファイルへのポインターを含み、.dbg ファイルが .pdb ファイルへのポインターを格納します。

古いシンボル ファイル システムを使用して、2 つのファイルの配置と 3 つのファイルの配置の両方と同じ実行可能コードと同じシンボルを含めます。 プログラムを実行し、いずれかの方法で配置をデバッグできます。 ただし、実行可能ファイルが小さいために、3 つのファイルの配置は、実行が速くなります。

2 ファイル arrangment で古いシンボル ファイル システムでビルドされたバイナリがあれば、BinPlace に変換できます、3 つのファイルの配置。 つまり、BinPlace できます「分割」シンボルのない実行可能ファイルに実行可能ファイルと、実行可能ファイルに含まれていた、シンボルを含む新しい .dbg ファイル。

BinPlace も、ファイルを分割すること、また場合だけ古いシンボル ファイル システム、ファイルからプライベート シンボル情報を取り除くことができます (つまり、2 つのファイルの配置からファイルが変更する 3 つのファイルの配置に場合にのみ)。 BinPlace ことはできません古いシンボル ファイル システム内のファイルからプライベート シンボルを削除し、2 つのファイルの配置のままにします。 ファイルが 3 つのファイルの配置で既に場合 BinPlace 行われない任意の分解です。実際はも移動されません、シンボル ファイル BinPlace コマンドラインで実行可能ファイルがという名前の場合。 参照してください[パブリック シンボルとプライベート シンボルの](public-symbols-and-private-symbols.md)詳細についてはします。

 

 





