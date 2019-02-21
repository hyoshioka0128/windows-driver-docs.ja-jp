---
title: '[ウォッチ] ウィンドウで変数を制御します。'
description: '[ウォッチ] ウィンドウで変数を制御します。'
ms.assetid: bd857442-fbd7-4c00-9743-6077d38ee38e
keywords:
- ウォッチ ウィンドウで、グローバル変数
- ウォッチ ウィンドウ、ローカル変数
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9fd952b95525585095a9008dcdfef5c5ca7c6a92
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558073"
---
# <a name="controlling-variables-through-the-watch-window"></a>[ウォッチ] ウィンドウで変数を制御します。


## <span id="ddk_debugging_bios_code_dbg"></span><span id="DDK_DEBUGGING_BIOS_CODE_DBG"></span>


、WinDbg で表示し、グローバルとローカル変数を変更する [ウォッチ] ウィンドウを使用することもできます。

[ウォッチ] ウィンドウには、使用する変数の一覧を表示できます。 これらの変数には、グローバル変数と任意の関数からのローカル変数を含めることができます。 [ウォッチ] ウィンドウでは、いつでも、現在の関数のスコープに一致する変数の値を表示します。 [ウォッチ] ウィンドウでこれらの変数の値を変更することもできます。

[ウォッチ] ウィンドウは、[ローカル] ウィンドウとは異なり、ローカル コンテキストの変更により影響はありません。 現在のプログラム カウンターのスコープで定義されている変数のみには、表示または変更は、その値を持つことができます。

 

 





