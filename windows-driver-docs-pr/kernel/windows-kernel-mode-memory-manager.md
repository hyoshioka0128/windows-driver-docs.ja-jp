---
title: Windows カーネルモード メモリ マネージャー
description: Windows カーネルモード メモリ マネージャー
ms.assetid: ab464d5b-7bad-494e-80cd-e32ca9e9fa8d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8984b98fcc399c587d8c9c6c8511d9b9aaced9a3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571038"
---
# <a name="windows-kernel-mode-memory-manager"></a>Windows カーネルモード メモリ マネージャー


Windows カーネル モードのメモリ マネージャー コンポーネントは、オペレーティング システムの物理メモリを管理します。 このメモリは、主にランダム アクセス メモリ (RAM) の形式でです。

メモリ マネージャーは、次の主要なタスクを実行することによってメモリを管理します。

-   事実上、動的に割り当てとメモリの解放を管理します。

-   メモリ マップト ファイルは、共有メモリ、およびコピー オン ライトの概念をサポートします。

ドライバーのメモリ管理についての詳細を参照してください。 [Windows ドライバーのメモリ管理](managing-memory-for-drivers.md)します。

メモリ マネージャーに直接インターフェイスを提供するルーチンには文字で、通常、プレフィックス"**Mm**"。 たとえば、 **MmGetPhysicalAddress**します。 メモリ マネージャー ルーチンの一覧は、[Memory Manager ルーチン](https://msdn.microsoft.com/library/windows/hardware/ff554435)を参照してください。

機能によって並べ替えられた、メモリ マネージャー ルーチンのリストは、[メモリの割り当てとバッファー管理](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_kernel/#memory-allocation-and-buffer-management)を参照してください。

 

 




