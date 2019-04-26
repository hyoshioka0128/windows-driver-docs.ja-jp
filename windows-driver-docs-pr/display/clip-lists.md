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
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354322"
---
# <a name="clip-lists"></a>クリップ リスト


## <span id="ddk_clip_lists_gg"></span><span id="DDK_CLIP_LISTS_GG"></span>


クリップされた blt は、Microsoft Windows 2000 以降では、ドライバーに渡されることはありません。 **IsClipped**のメンバー [ **DD\_BLTDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff550474)は常に**FALSE**、常に、クリップされた一覧と**NULL**します。

 

 





