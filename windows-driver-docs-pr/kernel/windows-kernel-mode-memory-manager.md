---
title: Windows カーネルモード メモリ マネージャー
description: Windows カーネルモード メモリ マネージャー
ms.assetid: ab464d5b-7bad-494e-80cd-e32ca9e9fa8d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1674bbdfdc7c54997489f6478ab56547739dc8a8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835721"
---
# <a name="windows-kernel-mode-memory-manager"></a>Windows カーネルモード メモリ マネージャー


Windows カーネルモードのメモリマネージャーコンポーネントは、オペレーティングシステムの物理メモリを管理します。 このメモリは主にランダムアクセスメモリ (RAM) の形式です。

メモリマネージャーは、次の主なタスクを実行してメモリを管理します。

-   仮想的および動的なメモリの割り当てと解放を管理します。

-   メモリマップトファイル、共有メモリ、および書き込み時コピーの概念をサポートします。

ドライバーのメモリ管理の詳細については、「 [Windows ドライバーのメモリ管理](managing-memory-for-drivers.md)」を参照してください。

メモリマネージャーに直接インターフェイスを提供するルーチンには、通常、文字 "**Mm**" が付いています。たとえば、 **MmGetPhysicalAddress**のようになります。 Memory manager ルーチンの一覧については、「 [Memory Manager ルーチン](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554435(v=vs.85))」を参照してください。

機能によって並べ替えられた memory manager ルーチンの一覧については、「[メモリ割り当てとバッファー管理](https://docs.microsoft.com/windows-hardware/drivers/ddi/_kernel/#memory-allocation-and-buffer-management)」を参照してください。

 

 




