---
title: クリップ リスト
description: クリップ リスト
ms.assetid: 73383093-ab83-4955-b017-cc370009fd0e
keywords:
- サーフェス WDK DirectDraw、中
- 描画 blt WDK DirectDraw、クリップ リスト
- DirectDraw 中 WDK Windows 2000 の表示クリップを一覧表示します。
- WDK DirectDraw、クリップ リストの中
- blt WDK DirectDraw、クリップ リスト
- クリップは、WDK DirectDraw を一覧表示します。
- クリップ blt WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f10669cfae7b403840832cd5b4ed9362da32004
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370702"
---
# <a name="clip-lists"></a>クリップ リスト


## <span id="ddk_clip_lists_gg"></span><span id="DDK_CLIP_LISTS_GG"></span>


クリップされた blt は、Microsoft Windows 2000 以降では、ドライバーに渡されることはありません。 **IsClipped**のメンバー [ **DD\_BLTDATA** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_bltdata)は常に**FALSE**、常に、クリップされた一覧と**NULL**します。

 

 





