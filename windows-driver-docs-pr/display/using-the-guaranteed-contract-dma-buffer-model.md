---
title: 保証されたコントラクト DMA バッファー モデルの使用
description: 保証されたコントラクト DMA バッファー モデルの使用
ms.assetid: fee6f7eb-157b-466d-b482-110a48045283
keywords:
- DMA バッファー WDK 表示、保証されたコントラクトモード
- 保証されたコントラクト DMA バッファーの WDK 表示
- パッチ-場所リスト WDK 表示
ms.date: 10/11/2019
ms.localizationpriority: medium
ms.openlocfilehash: e62bcabe753a0c92422e326422076ab71b7c77bf
ms.sourcegitcommit: d57f3ad976393a2c5dffc05851a0314858ce05e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/11/2019
ms.locfileid: "72280265"
---
# <a name="using-the-guaranteed-contract-dma-buffer-model"></a>保証されたコントラクト DMA バッファー モデルの使用

Windows Vista のディスプレイドライバーモデルは、レンダリングデバイスの DMA バッファーと修正プログラムの場所の一覧のサイズを保証します。 修正プログラムの場所の一覧には、DMA バッファー内のコマンドによって参照されるリソースの物理メモリアドレスが含まれています。

保証されたコントラクトモードでは、ユーザーモードの表示ドライバーは、ユーザーモードのディスプレイドライバーによってコマンドバッファーがいっぱいになった[**ときに、** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb)変換に使用できる DMA バッファーと修正プログラムの場所のリストの正確なサイズを認識します。ディスプレイミニポートドライバー。 **Pfnrendercb**を呼び出すたびに、ユーザーモード表示ドライバーは、次の変換に使用できる DMA バッファーと修正プログラムの場所リストのサイズを受け取ります (つまり、 **pfnrendercb**への次の呼び出し)。

ビデオメモリマネージャーは、次の変換が完了するまで、そのデバイスの DMA バッファーと修正プログラムの場所の一覧をトリミングしないことを保証します。 ディスプレイミニポートドライバーは、1つのコマンドバッファーを1つの DMA バッファーと1つの修正プログラムの場所の一覧に変換できる必要があります。 この変換ができない場合、ユーザーモードのコマンドバッファーは定義上、無効になります。 表示ミニポートドライバーは、変換中に DMA バッファー領域と修正プログラムの場所の一覧から外れていることを示す状態を返すことができません。これにより、メモリマネージャーが保証された DMA コントラクトの要件を満たしていなかったため、video memory manager のバグチェックが行われます。
