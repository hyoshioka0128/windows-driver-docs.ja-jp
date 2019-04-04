---
title: ファイル システムの参照とシンボル ファイル
description: ファイル システムの参照とシンボル ファイル
ms.assetid: c667380f-2942-453c-9ec8-70d3e1355e72
keywords:
- SymStore、短いファイル名
- 短いファイル名と SymStore
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d079eda2b815270ee37f367a9fcb6b7262fd855
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578533"
---
# <a name="file-system-references-and-symbol-files"></a>ファイル システムの参照とシンボル ファイル


## <span id="ddk_symbol_files_overview_dbg"></span><span id="DDK_SYMBOL_FILES_OVERVIEW_DBG"></span>


ディスク上のファイルには、長いファイル名と自動的に生成された省略 MS-DOS 互換性のある 8.3 短いファイル名の両方を持つことができます。 シンボル ファイルをシンボル ストアに追加した後、そのシンボル ファイル内のシンボルする可能性があるないアクセス可能なデバッグ中にシンボル ファイルには、任意の省略 MS-DOS 8.3 ファイル名が含まれている場合は。

ツールは、シンボル ファイルを作成するときに、シンボル ファイルのデバッグ レコードに記録されているファイル名のバージョンは、ツール、および実行する方法によって異なります。 ファイルの省略名がシステムによって異なるためシンボル ファイルに組み込まれているレコードの実際のファイル名ではなく省略の MS-DOS 8.3 ファイル名がある場合に、シンボルの読み込み時にデバッグで問題が発生します。 この問題が発生した場合は、これらのシンボル ファイルの内容アクセスできないデバッグ中にします。 可能であれば、ユーザーがからシンボル ファイルを作成するときに省略ファイルのパス名を使用しないようにします。 ファイルの省略名を誤って使用するいくつかの点がソース ファイルの場合省略ファイルのパス名を使用する、*含める*ディレクトリ、またはライブラリが含まれるファイル。

詳細については、[シンボル名の一致する](matching-symbol-names.md)を参照してください。

 

 





