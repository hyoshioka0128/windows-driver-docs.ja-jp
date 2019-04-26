---
title: ローカル変数へのアクセス
description: ローカル変数へのアクセス
ms.assetid: 0aab3fdf-fe0c-46ad-aa2f-90992811b001
keywords:
- ローカル変数へのアクセス
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 505ee2fd9b253aa145410ce4c101ee2b41cce713
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351517"
---
# <a name="accessing-local-variables"></a>ローカル変数へのアクセス


## <span id="ddk_debugging_bios_code_dbg"></span><span id="DDK_DEBUGGING_BIOS_CODE_DBG"></span>


グローバル変数などのローカル変数は、シンボル ファイルに格納されます。 され、グローバル変数と同様、デバッガーにはアドレスとして、名前が解釈されます。 これらは、読み取りし、グローバル変数と同じ方法で書き込みが可能です。 ただし、シンボルがローカル コマンドに示すために必要がある場合の前にドル記号 ($) とシンボル、感嘆符 (! )、うに`$!var`します。

Visual Studio と WinDbg を表示およびローカル変数の編集 (コマンド) だけでなく使用できるユーザー インターフェイス要素を提供します。 詳細については、次を参照してください。[表示と編集のメモリと Visual Studio でのレジスタ](viewing-memory--variables--and-registers-in-visual-studio.md)と[表示し、WinDbg でローカル変数の編集](locals-window.md)します。

表示、変更、およびローカル変数を使用して、次のメソッドを使用することもできます。

-   [ **Dv (ローカル変数の表示)** ](dv--display-local-variables-.md)コマンドは、名前とすべてのローカル変数の値が表示されます。

-   [ **! の\_各\_ローカル**](-for-each-local.md)拡張機能では、1 つのコマンドを繰り返し実行、1 回の各ローカル変数をことができます。

ただし、ローカルとグローバル変数の 1 つの主な違いがあります。 アプリケーションを実行しているときに、ローカル変数の意味は、このような変数のスコープが定義されている関数にのみ拡張するため、プログラム カウンターの場所に依存します。

デバッガーによるローカル変数の解釈、[ローカル コンテキスト](changing-contexts.md#local-context)します。 既定では、このコンテキストは、プログラムのカウンターの場所と一致します。 デバッガーは、コンテキストを変更できます。 ローカル コンテキストの詳細については、ローカル コンテキストを参照してください。

ローカル コンテキストが変更されたときにローカル変数の新しいコレクションを反映するように、[ローカル] ウィンドウがすぐに更新されます。 [ **Dv** ](dv--display-local-variables-.md)コマンドでは、新しい変数も表示されます。 前に説明したメモリのコマンドでは、すべてのこれらの変数名が正しく解釈し、します。 読み取るしたり、これらの変数を作成できます。

 

 





