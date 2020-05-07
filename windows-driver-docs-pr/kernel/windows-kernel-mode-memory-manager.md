---
title: Windows カーネルモード メモリ マネージャー
description: Windows カーネルモード メモリ マネージャー
ms.assetid: ab464d5b-7bad-494e-80cd-e32ca9e9fa8d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 63b26330ec14e15c1fd536eeb1459e4953ac07d9
ms.sourcegitcommit: 6e2986506940c203a6a834a927a774b7efa6b86e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/05/2020
ms.locfileid: "82800099"
---
# <a name="windows-kernel-mode-memory-manager"></a>Windows カーネルモード メモリ マネージャー


Windows カーネルモードのメモリマネージャーコンポーネントは、オペレーティングシステムの物理メモリを管理します。 このメモリは主にランダムアクセスメモリ (RAM) の形式です。

メモリマネージャーは、次の主なタスクを実行してメモリを管理します。

-   仮想的および動的なメモリの割り当てと解放を管理します。

-   メモリマップトファイル、共有メモリ、および書き込み時コピーの概念をサポートします。

ドライバーのメモリ管理の詳細については、「 [Windows ドライバーのメモリ管理](managing-memory-for-drivers.md)」を参照してください。

メモリマネージャーに直接インターフェイスを提供するルーチンには、通常、文字 "**Mm**" が付いています。たとえば、 **MmGetPhysicalAddress**のようになります。 Memory manager ルーチンに関するドキュメントを検索するには、 [**MmAdvanceMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmadvancemdl)に移動し、左側の目次を使用して、Mm * ルーチンをスクロールします。

機能によって並べ替えられた memory manager ルーチンの一覧については、「[メモリ割り当てとバッファー管理](https://docs.microsoft.com/windows-hardware/drivers/ddi/_kernel/#memory-allocation-and-buffer-management)」を参照してください。

 

 




