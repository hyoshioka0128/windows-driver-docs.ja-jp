---
title: ユーザー モードからカーネル モードに送信されるプライベート データの検証
description: ユーザー モードからカーネル モードに送信されるプライベート データの検証
ms.assetid: 7022af7b-80e7-41a5-bd53-32d7eafc4062
keywords:
- プライベートデータの WDK 表示の検証
- プライベートデータ検証 WDK ディスプレイ
- プライベートデータの WDK 表示が無効です
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 358c78073b9debafad01fb867c2fdfbf47cd0424
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829226"
---
# <a name="validating-private-data-sent-from-user-mode-to-kernel-mode"></a>ユーザー モードからカーネル モードに送信されるプライベート データの検証


表示ミニポートドライバーは、ユーザーモードの表示ドライバーから送信されるすべてのプライベートデータを検証して、プライベートデータが無効な場合に、ミニポートドライバーがクラッシュしたり、応答したり (ハング)、アサートしたり、メモリを破損したりしないようにする必要があります。 ただし、オペレーティングシステムによって "ハング" されるハードウェアがリセットされるため、ディスプレイミニポートドライバーは、GPU が "ハング" する原因となっているグラフィックス処理ユニット (GPU) に命令を送信できます。 プライベートデータには、次のいずれかの項目を含めることができます。

-   [**Dxgkarg\_RENDER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_render)構造体の**pcommand** buffer メンバーの[**DxgkDdiRender**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_render)または[**DxgkDdiRenderKm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_renderkm)関数に送信されたコマンドバッファーの内容。

-   次のミニポートドライバー機能に送信されるデータ:
    -   [**DxgkDdiCreateAllocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation)関数は、 [**Dxgkarg**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_createallocation)の**pprivatedriverdata** buffer メンバーで、CREATEALLOCATION と[**DXGK\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_allocationinfo)の割り当て情報の構造体を\_します。
    -   [**DxgkDdiEscape**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_escape)関数は、 [**Dxgkarg**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_escape)の**pprivatedriverdata** buffer メンバーに含まれている\_エスケープ構造体です。
    -   [**Dxgkarg\_ACQUIRESWIZZLINGRANGE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_acquireswizzlingrange)構造体の**privatedriverdata** 32-bit メンバーの[**DxgkDdiAcquireSwizzlingRange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_acquireswizzlingrange)関数。
    -   [**Dxgkarg\_RELEASESWIZZLINGRANGE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_releaseswizzlingrange)構造体の**privatedriverdata** 32-bit メンバーの[**DxgkDdiReleaseSwizzlingRange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_releaseswizzlingrange)関数。
    -   DXGKQAITYPE\_UMDRIVERPRIVATE 値が**型**のメンバーに指定されている場合、 [**Dxgkarg\_queryadapterinfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_queryadapterinfo)構造体の**Pinputdata** buffer メンバーの[**DxgkDdiQueryAdapterInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryadapterinfo)関数。

 

 





