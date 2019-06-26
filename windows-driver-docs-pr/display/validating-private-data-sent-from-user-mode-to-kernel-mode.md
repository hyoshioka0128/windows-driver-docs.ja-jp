---
title: ユーザー モードからカーネル モードに送信されるプライベート データの検証
description: ユーザー モードからカーネル モードに送信されるプライベート データの検証
ms.assetid: 7022af7b-80e7-41a5-bd53-32d7eafc4062
keywords:
- WDK の表示、プライベート データの検証
- プライベート データ検証 WDK の表示
- 無効なプライベート データ WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: df699cc66135a029553fe0c0fd690fecbdd40157
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374359"
---
# <a name="validating-private-data-sent-from-user-mode-to-kernel-mode"></a>ユーザー モードからカーネル モードに送信されるプライベート データの検証


ディスプレイのミニポート ドライバーする必要がありますすべてプライベート データ検証ミニポート ドライバーがクラッシュしていることを防ぐために、ユーザー モードのディスプレイ ドライバーから送信された応答していない (ハング) アサート、またはプライベート データが有効でない場合、メモリの破損します。 ただし、オペレーティング システムでは、「ハング」ハードウェアがリセットされ、ため、表示ミニポート ドライバーに送信する手順については GPU が「ハング」が発生するグラフィックス処理装置 (GPU) プライベート データは、次のものを含めることができます。

-   ミニポート ドライバーの送信バッファーの内容をコマンド[ **DxgkDdiRender** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_render)または[ **DxgkDdiRenderKm** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_renderkm)関数で、 **pCommand**のバッファーのメンバー、 [ **DXGKARG\_レンダリング**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_render)構造体。

-   次のミニポート ドライバー関数に送信されるデータ:
    -   [ **DxgkDdiCreateAllocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation)で機能、 **pPrivateDriverData**バッファーのメンバー、 [ **DXGKARG\_CREATEALLOCATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_createallocation)と[ **DXGK\_ALLOCATIONINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_allocationinfo)構造体。
    -   [ **DxgkDdiEscape** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_escape)で機能、 **pPrivateDriverData**のバッファーのメンバー、 [ **DXGKARG\_エスケープ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_escape)構造体。
    -   [ **DxgkDdiAcquireSwizzlingRange** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_acquireswizzlingrange)で機能、 **PrivateDriverData**の 32 ビットのメンバー、 [ **DXGKARG\_ACQUIRESWIZZLINGRANGE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_acquireswizzlingrange)構造体。
    -   [ **DxgkDdiReleaseSwizzlingRange** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_releaseswizzlingrange)で機能、 **PrivateDriverData**の 32 ビットのメンバー、 [ **DXGKARG\_RELEASESWIZZLINGRANGE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_releaseswizzlingrange)構造体。
    -   [ **DxgkDdiQueryAdapterInfo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_queryadapterinfo)で機能、 **pInputData**のバッファーのメンバー、 [ **DXGKARG\_QUERYADAPTERINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_queryadapterinfo)ときに構造体、DXGKQAITYPE\_UMDRIVERPRIVATE 値で指定、**型**メンバー。

 

 





