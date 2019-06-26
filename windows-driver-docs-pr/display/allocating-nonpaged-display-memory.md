---
title: 非ページ表示メモリの割り当て
description: 非ページ表示メモリの割り当て
ms.assetid: 6a8523e7-3955-4289-b131-52556ba3e631
keywords:
- WDK DirectX 9.0 の非ページの表示メモリ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 987bdd6d6abd870439a94372dc6fa2bff1bcb357
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384647"
---
# <a name="allocating-nonpaged-display-memory"></a>非ページ表示メモリの割り当て


## <span id="ddk_allocating_nonpaged_display_memory_gg"></span><span id="DDK_ALLOCATING_NONPAGED_DISPLAY_MEMORY_GG"></span>


**このトピックでは、Microsoft Windows XP にのみ以降に適用されます。**

DirectX 9.0 バージョンのディスプレイ ドライバーが呼び出すことができます、 [ **EngAllocMem** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engallocmem)からシステムのメモリを割り当てるだけでなく、グラフィックス デバイス インターフェイス (GDI) 関数のページの非ページ プールからも対象プール。 非ページ メモリを割り当てるには、ドライバーが、FL を指定する必要があります\_非ページ\_メモリ フラグ、*フラグ*のパラメーター、 **EngAllocMem**呼び出します。 このフラグが指定されていない場合は、システムのページ プールからメモリが割り当てられます。

Windows 2000 と前から、システムの唯一の許可されている割り当てページ プール

非ページ プールから割り当てるには、この機能は、以降 WindowsXP で利用可能でしたが、Windows XP と Windows XP Service Pack 1 (SP1) Ddk が記載いません。

 

 





