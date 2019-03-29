---
title: DMA モデルの非ローカルの表示メモリに対するフラグ設定のサポート
description: DMA モデルの非ローカルの表示メモリに対するフラグ設定のサポート
ms.assetid: 7310bf92-a1bb-4a72-8e1a-bae7e656a499
keywords:
- DMA スタイル AGP WDK DirectDraw
- 表示メモリ WDK DirectDraw、DMA スタイル AGP
- 非ローカルの表示メモリ WDK DirectDraw、DMA スタイル AGP
- AGP WDK DirectDraw、DMA スタイル AGP
- 描画の AGP サポート WDK DirectDraw、DMA スタイル AGP
- DirectDraw AGP サポート DMA スタイル AGP、WDK の Windows 2000 の表示
- メモリ WDK DirectDraw AGP、DMA スタイル AGP
- WDK DirectDraw 非ローカル メモリにフラグを設定します。
- DDCAPS2_NONLOCALVIDMEM
- DDCAPS2_NONLOCALVIDMEMCAPS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 014f96f31bff351ab66ba6e6464362c47f6d9474
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578006"
---
# <a name="flagging-support-for-dma-model-nonlocal-display-memory"></a>DMA モデルの非ローカルの表示メモリに対するフラグ設定のサポート


## <span id="ddk_flagging_support_for_dma_model_nonlocal_display_memory_gg"></span><span id="DDK_FLAGGING_SUPPORT_FOR_DMA_MODEL_NONLOCAL_DISPLAY_MEMORY_GG"></span>


DDCAPS2 を指定するだけでなく\_AGP を報告する NONLOCALVIDMEM フラグのサポートは、DMA モデルのドライバーは、機能フラグ DDCAPS2 をエクスポートする必要があります\_NONLOCALVIDMEMCAPS します。 このフラグは、(AGP) の非ローカル メモリにローカルの表示メモリよりもさまざまな機能を示します。

 

 





