---
title: WinDbg でのグローバル変数の表示と編集
description: WinDbg でのグローバル変数の表示と編集
ms.assetid: 4273F6D8-A2A1-43FA-80BF-97E5673FAF05
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a559fb816042a272e0430f58ec02c96828799448
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348945"
---
# <a name="viewing-and-editing-global-variables-in-windbg"></a>WinDbg でのグローバル変数の表示と編集


## <span id="ddk_debugging_bios_code_dbg"></span><span id="DDK_DEBUGGING_BIOS_CODE_DBG"></span>


デバッガーは、仮想アドレスとして、グローバル変数の名前を解釈します。 すべての記載されているコマンドを使用するため、[仮想アドレスにアクセスするメモリ](accessing-memory-by-virtual-address.md)グローバル変数を読み書きします。

さらに、使用、 [**でしょうか。(式の評価)** ](---evaluate-expression-.md)任意のシンボルに関連付けられているアドレスを表示するコマンド。

、WinDbg で表示し、グローバルとローカル変数を変更する [ウォッチ] ウィンドウを使用することもできます。 [ウォッチ] ウィンドウには、使用する変数の一覧を表示できます。 これらの変数には、グローバル変数と任意の関数からのローカル変数を含めることができます。 [ウォッチ] ウィンドウでは、いつでも、現在の関数のスコープに一致する変数の値を表示します。 [ウォッチ] ウィンドウでこれらの変数の値を変更することもできます。

[ウォッチ] ウィンドウを開くには、次のように選択します。**ウォッチ**から、**ビュー**メニュー。 ALT + 2 キーを押すこともできますかをクリックして、**ウォッチ**ツールバーのボタン:![ウォッチ式のボタンのスクリーン ショット](images/tbwatch.png)します。 ALT + SHIFT + 2 は、[ウォッチ] ウィンドウを閉じます。

次のスクリーン ショットでは、ウォッチ ウィンドウの例を示します。

![[ウォッチ] ウィンドウのスクリーン ショット ](images/window-watch.png)

[ウォッチ] ウィンドウには、4 つの列を含めることができます。 **名前**と**値**列は常に表示される、および**型**と**場所**列は省略可能です。 表示する、**型**と**場所**列、をクリックして、 **Typecast**と**場所**ボタン、それぞれ、ツールバーの。

 

 





