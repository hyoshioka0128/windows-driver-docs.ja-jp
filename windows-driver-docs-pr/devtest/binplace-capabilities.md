---
title: BinPlace 機能
description: BinPlace 機能
ms.assetid: 2fd49ce3-8617-4c3e-bb86-8642343ca756
keywords:
- BinPlace WDK、機能
- ファイルの削除
- ファイルの分割
- WDK BinPlace ファイルの移動
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44deb199bc411e6015573d5c121f83ec1e1bfbfe
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531471"
---
# <a name="binplace-capabilities"></a>BinPlace 機能


## <span id="ddk_binplace_capabilities_tools"></span><span id="DDK_BINPLACE_CAPABILITIES_TOOLS"></span>


BinPlace は主に 3 つのアクションを実行します。 ファイル、ファイルを分割すると、ファイルの移動を削除します。

### <a name="span-idstrippingfilesspanspan-idstrippingfilesspanstripping-files"></a><span id="stripping_files"></span><span id="STRIPPING_FILES"></span>ファイルの削除

コンパイラとリンカーが作成されるシンボルは、2 つのカテゴリに分類できます。 パブリック シンボルとプライベート シンボル。 シンボル ファイルを削除、プライベート シンボル情報を削除し、パブリック シンボル情報だけが残ります。

詳細については、次を参照してください。[パブリック シンボルとプライベート シンボルの](public-symbols-and-private-symbols.md)します。

### <a name="span-idsplittingfilesspanspan-idsplittingfilesspansplitting-files"></a><span id="splitting_files"></span><span id="SPLITTING_FILES"></span>ファイルの分割

いくつかの実行可能ファイルには、シンボルが含まれています。 BinPlace は、この種のファイルを 2 つのファイルに分割することができます。

-   実行可能コードがないシンボル ファイル

-   シンボル情報のない実行可能ファイル

詳細については、次を参照してください。[シンボル ファイル システム](symbol-file-systems.md)します。

### <a name="span-idmovingfilesspanspan-idmovingfilesspanmoving-files"></a><span id="moving_files"></span><span id="MOVING_FILES"></span>ファイルの移動

BinPlace には、ファイルを移動できます。 BinPlace は実行可能ファイル以外の任意のファイルで使用するときは、その内容を変更することがなく、移行先のディレクトリ ツリーを移動、されます。

BinPlace は、実行可能ファイルで使用すると、同じディレクトリに、関連付けられているシンボル ファイルが、実行可能ファイルとシンボル ファイルのどちらも移動されます。 削除または分割は、適切な BinPlace オプションが選択されている場合にも発生します。

大規模なプロジェクトの場合は、適切なプロジェクト ディレクトリに多数のファイルを整理する BinPlace を使用できます。 大規模な一連のバイナリ ファイルを作成する別のパッケージ ファイルのさまざまなサブセットを収集する場合は、BinPlace はこのプロセスを管理できます。

詳細については、次を参照してください。 [BinPlace コピー先のディレクトリ](binplace-destination-directories.md)します。

 

 





