---
title: 非標準の表示モードのサポート
description: 非標準の表示モードのサポート
ms.assetid: 33a10aed-dfc9-4b64-97fb-e4b7c744dc0d
keywords:
- WDK DirectX 9.0 の非表示モード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f56ef493d16ceda5ee3b055a76164a41c82b4af6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350216"
---
# <a name="supporting-nonstandard-display-modes"></a>非標準の表示モードのサポート


## <span id="ddk_supporting_nonstandard_display_modes_gg"></span><span id="DDK_SUPPORTING_NONSTANDARD_DISPLAY_MODES_GG"></span>


10-bits-ごとのチャネル (10:10:10:2) など、任意の非標準の表示モードをサポートするデバイスのバージョンのドライバーが表示され、ターゲットの形式の表示は、DirectX 9.0 は、これらの拡張の非表示モードを列挙する要求に応答する必要があります。 さらに、DirectX 9.0 ドライバーは、標準および非標準の表示モードの切り替えを有効にする操作を実行できる必要があります。 次のセクションでは、ドライバーが非表示モードをサポートする方法について説明します。

[拡張形式を列挙します。](enumerating-extended-formats.md)

[標準および非標準モードの切り替え](switching-between-standard-and-nonstandard-modes.md)

[非標準の表示モードの処理](handling-nonstandard-display-modes.md)

 

 





