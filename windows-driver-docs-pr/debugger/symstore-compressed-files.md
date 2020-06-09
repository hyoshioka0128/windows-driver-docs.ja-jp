---
title: SymStore の圧縮ファイル
description: SymStore の圧縮ファイル
ms.assetid: 4ec6a7f5-ceee-46d5-9a5e-36ab9fe9db52
keywords:
- SymStore、圧縮ファイル
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 401e1d86c46436bb21639ea4fe60845003973ddc
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84533921"
---
# <a name="symstore-compressed-files"></a>SymStore の圧縮ファイル


## <span id="ddk_symbol_files_overview_dbg"></span><span id="DDK_SYMBOL_FILES_OVERVIEW_DBG"></span>


SymStore は、次の2つの方法で圧縮ファイルと共に使用できます。

1.  SymStore を **/p**オプションと共に使用して、シンボルファイルへのポインターを格納します。 SymStore が完了したら、ポインターが参照するファイルを圧縮します。

2.  SymStore を **/x**オプションと共に使用して、インデックスファイルを作成します。 SymStore が完了したら、インデックスファイルに示されているファイルを圧縮します。 次に、SymStore を **/y**オプションと共に使用し (必要に応じて **/p**オプションを使用して)、ファイルまたはポインターをシンボルストアに格納します。 (SymStore は、この操作を実行するためにファイルを圧縮解除する必要はありません)。

シンボルサーバーは、適切なタイミングでファイルの圧縮を解除します。

シンボルサーバーとして SymSrv を使用している場合は、[ここで](https://www.microsoft.com/download/details.aspx?displaylang=en&id=17657 )提供されている compress ツールを使用して圧縮を行う必要があります。 圧縮ファイルには、ファイル拡張子の最後の文字としてアンダースコア (たとえば、 \_ module2 または) を指定する必要があり \_ ます。 詳細については、「 [Symsrv](symsrv.md)」を参照してください。

 

 





