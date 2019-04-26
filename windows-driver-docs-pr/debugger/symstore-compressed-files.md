---
title: SymStore の圧縮ファイル
description: SymStore の圧縮ファイル
ms.assetid: 4ec6a7f5-ceee-46d5-9a5e-36ab9fe9db52
keywords:
- SymStore、圧縮されたファイル
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22ad34cdb4e93e6d9376f0870e33543c2bfa2804
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335458"
---
# <a name="symstore-compressed-files"></a>SymStore の圧縮ファイル


## <span id="ddk_symbol_files_overview_dbg"></span><span id="DDK_SYMBOL_FILES_OVERVIEW_DBG"></span>


SymStore は、2 つの方法で、圧縮ファイルで使用できます。

1.  SymStore でを使用して、 **/p**シンボル ファイルへのポインターを格納するオプション。 SymStore が完了したら後、は、ポインターが参照するファイルを圧縮します。

2.  SymStore でを使用して、 **/x**インデックス ファイルを作成するオプション。 SymStore が完了すると、インデックス ファイルに示されているファイルを圧縮します。 SymStore を次に、使用、 **/y**オプション (を希望されない場合、 **/p**オプション) シンボル ストアにファイルまたはファイルへのポインターを格納します。 (SymStore は必要ありません、この操作を実行するファイルの圧縮を解除する)。

シンボル サーバーは、適切な時にファイルを圧縮解除の責任になります。

圧縮を行う必要があります SymSrv としてシンボル サーバーを使用している場合は compress.exe ツールを使用して[ここ](https://go.microsoft.com/fwlink/p/?linkid=239917)。 圧縮されたファイルでは、それらのファイル拡張子の最後の文字として、アンダー スコアが必要 (たとえば、module1.pd\_または module2.db\_)。 詳細については、次を参照してください。 [SymSrv](symsrv.md)します。

 

 





