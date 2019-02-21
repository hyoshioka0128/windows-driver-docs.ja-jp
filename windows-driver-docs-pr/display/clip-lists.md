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
ms.openlocfilehash: dcb21390ea3a0a40403f643746c8ea5bc38f2106
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558200"
---
# <a name="clip-lists"></a>クリップ リスト


## <span id="ddk_clip_lists_gg"></span><span id="DDK_CLIP_LISTS_GG"></span>


クリップされた blt は、Microsoft Windows 2000 以降では、ドライバーに渡されることはありません。 **IsClipped**のメンバー [ **DD\_BLTDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff550474)は常に**FALSE**、常に、クリップされた一覧と**NULL**します。

 

 





