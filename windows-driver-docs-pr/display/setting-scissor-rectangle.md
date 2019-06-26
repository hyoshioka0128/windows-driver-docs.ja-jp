---
title: シザー矩形の設定
description: シザー矩形の設定
ms.assetid: e85b4987-26b7-4005-b8eb-81ca36a9a777
keywords:
- シザリング四角形 WDK DirectX 9.0
- 四角形のクリッピング領域 WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09cbd39d49a2b0acebbd8159c8e877f42ee39a99
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365563"
---
# <a name="setting-scissor-rectangle"></a>シザー矩形の設定


## <span id="ddk_setting_scissor_rectangle_gg"></span><span id="DDK_SETTING_SCISSOR_RECTANGLE_GG"></span>


DirectX 9.0 バージョンのドライバーでは、四角形のクリッピング領域、つまりシザリング四角形の設定をサポートする必要があります。 このシザリング四角形を設定すると、レンダリングはシザリング四角形で指定した、レンダー ターゲットの一部だけに限定されます。 シザリング四角形を設定するには、ドライバーが、D3DDP2OP を処理する必要があります\_SETSCISSORRECT 操作のコードでその[ **D3dDrawPrimitives2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)関数。 四角形のクリッピング領域を示す RECT 構造体で操作コードの後、[コマンド ストリーム](command-stream.md)します。

 

 





