---
title: 保証されたコントラクト DMA バッファー モデルの使用
description: 保証されたコントラクト DMA バッファー モデルの使用
ms.assetid: fee6f7eb-157b-466d-b482-110a48045283
keywords:
- DMA バッファー WDK 表示は、コントラクトのモードを保証
- WDK 表示コントラクト DMA バッファーの保証
- 更新プログラムの場所には、WDK の表示が一覧表示されます。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d554145854979b80ac46425dd138998daa42d1dd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381072"
---
# <a name="using-the-guaranteed-contract-dma-buffer-model"></a>保証されたコントラクト DMA バッファー モデルの使用


Windows Vista のディスプレイ ドライバー モデルは、DMA バッファーのサイズを保証し、レンダリング デバイスの更新プログラムの場所を一覧表示します。

保証されたコントラクト モードでは、ユーザー モードのディスプレイ ドライバーは、ユーザー モードのディスプレイ ドライバーがいっぱいになるコマンド バッファーと呼び出しに変換に使用される DMA バッファーと更新プログラムの場所の一覧の正確なサイズに注意してください[ **pfnRenderCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb)表示ミニポート ドライバーに送信します。 各呼び出しの後**pfnRenderCb**、ユーザー モードのディスプレイ ドライバーは、次の変換に使用される DMA バッファーと更新プログラムの場所の一覧のサイズを受け取る (これは、次の呼び出し**pfnRenderCb**).

ビデオ メモリ マネージャー DMA バッファーをトリミングするには、しないことを保証し、[次へ] の変換が完了するまで、そのデバイスの更新プログラムの場所を一覧表示します。 ディスプレイのミニポート ドライバーでは、1 つだけの DMA バッファーと 1 つの更新プログラムの場所の一覧に 1 つのコマンド バッファーを変換できる必要があります。 この変換ができない場合、ユーザー モード コマンド バッファーが、定義上が無効です。 ディスプレイのミニポート ドライバーは、DMA バッファー領域不足、;、変換時に更新プログラムの場所の一覧を示す状態を返すことはできません。保証された DMA コントラクトの要件を満たすメモリ マネージャーが失敗したため、システムを確認するビデオ メモリ マネージャーのバグになるので。

 

 





