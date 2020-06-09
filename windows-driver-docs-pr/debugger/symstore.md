---
title: SymStore
description: SymStore
ms.assetid: acc7bf3a-62ea-4c93-843e-b81d4f71555f
keywords:
- SymStore, 機能
- SymStore、使用
- シンボルストア、SymStore (SymStore)
ms.date: 03/27/2018
ms.localizationpriority: medium
ms.openlocfilehash: 46c8feeeac0d3c7a1b7e42a2d143f162bb11de47
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534289"
---
# <a name="symstore"></a>SymStore


## <span id="ddk_using_symstore_dbg"></span><span id="DDK_USING_SYMSTORE_DBG"></span>


SymStore (SymStore) は、シンボルストアを作成するためのツールです。 これは、Windows 用のデバッグツールに含まれています。 詳細については、「 [Windows 用デバッグツールのダウンロード](debugger-download-tools.md)」を参照してください。

SymStore は、シンボルを形式で格納します。これにより、デバッガーは、イメージのタイムスタンプとサイズ (dbg または実行可能ファイルの場合)、または署名と age (.pdb ファイル) に基づいてシンボルを検索できるようになります。 従来のシンボルストレージ形式に対するシンボルストアの利点は、すべてのシンボルを同じサーバーに格納または参照し、対応するシンボルがどの製品に含まれているかについての知識がなくても、デバッガーによって取得できることです。

複数のバージョンの .pdb シンボルファイル (たとえば、パブリックバージョンとプライベートバージョン) を同じサーバーに格納することはできません。それぞれに同じ署名と有効期間が含まれているためです。

ここでは、以下の内容について説明します。

[SymStore のトランザクション](symstore-transactions.md)

[ファイル システムの参照とシンボル ファイル](file-system-references-and-symbol-files.md)

[SymStore の圧縮ファイル](symstore-compressed-files.md)

[シンボル ストレージの形式](symbol-storage-format.md)

 

 





