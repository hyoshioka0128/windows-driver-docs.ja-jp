---
title: Windows カーネルモード メモリ マネージャー
description: Windows カーネルモード メモリ マネージャー
ms.assetid: ab464d5b-7bad-494e-80cd-e32ca9e9fa8d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: eb5728383445d9b803b8f12b05e8d7deba3082fc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358024"
---
# <a name="windows-kernel-mode-memory-manager"></a>Windows カーネルモード メモリ マネージャー


Windows カーネル モードのメモリ マネージャー コンポーネントは、オペレーティング システムの物理メモリを管理します。 このメモリは、主にランダム アクセス メモリ (RAM) の形式でです。

メモリ マネージャーは、次の主要なタスクを実行することによってメモリを管理します。

-   事実上、動的に割り当てとメモリの解放を管理します。

-   メモリ マップト ファイルは、共有メモリ、およびコピー オン ライトの概念をサポートします。

ドライバーのメモリ管理についての詳細を参照してください。 [Windows ドライバーのメモリ管理](managing-memory-for-drivers.md)します。

メモリ マネージャーに直接インターフェイスを提供するルーチンには文字で、通常、プレフィックス"**Mm**"。 たとえば、 **MmGetPhysicalAddress**します。 メモリ マネージャー ルーチンの一覧は、次を参照してください。 [Memory Manager ルーチン](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554435(v=vs.85))します。

機能によって並べ替えられた、メモリ マネージャー ルーチンのリストは、次を参照してください。[メモリの割り当てとバッファー管理](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_kernel/#memory-allocation-and-buffer-management)します。

 

 




