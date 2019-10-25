---
title: シザー矩形の設定
description: シザー矩形の設定
ms.assetid: e85b4987-26b7-4005-b8eb-81ca36a9a777
keywords:
- シザー四角形 WDK DirectX 9.0
- 四角形のクリッピング領域 WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93fa5db94bc32bea0811919565b45eb3e6a031b8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825823"
---
# <a name="setting-scissor-rectangle"></a>シザー矩形の設定


## <span id="ddk_setting_scissor_rectangle_gg"></span><span id="DDK_SETTING_SCISSOR_RECTANGLE_GG"></span>


DirectX 9.0 バージョンドライバーは、四角形のクリッピング領域、つまり、シザー四角形を設定することをサポートしている必要があります。 このシザー四角形を設定した後、レンダリングは、シザー四角形によって指定されるレンダーターゲットの部分のみに制限されます。 シザー四角形を設定するには、ドライバーで[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)関数の D3DDP2OP\_SETSCISSORRECT operation コードを処理する必要があります。 四角形のクリッピング領域を指定する RECT 構造体は、[コマンドストリーム](command-stream.md)の操作コードに従います。

 

 





