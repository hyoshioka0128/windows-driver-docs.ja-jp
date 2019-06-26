---
title: ストリーム バッファーと頂点バッファーのバインドの通知
description: ストリーム バッファーと頂点バッファーのバインドの通知
ms.assetid: 9ab9727f-053d-404b-95cc-ffd64fde7997
keywords:
- WDK の Windows 2000 の表示、複数のストリームの頂点の DirectX 8.0 リリース ノートします。
- 複数の頂点 WDK DirectX 8.0 をストリームします。
- 頂点 WDK DirectX 8.0 の複数のストリーム
- 頂点バッファー WDK DirectX 8.0
- 頂点へのバインドのストリーム バッファーの WDK DirectX 8.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27a8caba2ef2f8b90ec4329ed72dbbbb2b8401a9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372799"
---
# <a name="notification-of-stream-and-vertex-buffer-binding"></a>ストリーム バッファーと頂点バッファーのバインドの通知


## <span id="ddk_notification_of_stream_vertex_buffer_binding_gg"></span><span id="DDK_NOTIFICATION_OF_STREAM_VERTEX_BUFFER_BINDING_GG"></span>


ドライバーは、次のように新しい DP2 トークン D3DDP2OP で特定のストリームを頂点バッファーのバインドの通知\_SETSTREAMSOURCE、およびその関連付けられている HAL データ構造[ **D3DHAL\_DP2SETSTREAMSOURCE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_dp2setstreamsource).

 

 





