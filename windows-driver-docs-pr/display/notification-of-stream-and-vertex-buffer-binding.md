---
title: ストリーム バッファーと頂点バッファーのバインドの通知
description: ストリーム バッファーと頂点バッファーのバインドの通知
ms.assetid: 9ab9727f-053d-404b-95cc-ffd64fde7997
keywords:
- DirectX 8.0 リリースノート WDK Windows 2000 display、複数の頂点ストリーム
- 複数の頂点ストリーム (WDK DirectX 8.0)
- 頂点マルチストリーム WDK DirectX 8.0
- 頂点バッファー WDK DirectX 8.0
- 頂点バッファーへのストリームバインド WDK DirectX 8.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd84d46baa25b70ee776039fa5cba586bcdb7b85
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840528"
---
# <a name="notification-of-stream-and-vertex-buffer-binding"></a>ストリーム バッファーと頂点バッファーのバインドの通知


## <span id="ddk_notification_of_stream_vertex_buffer_binding_gg"></span><span id="DDK_NOTIFICATION_OF_STREAM_VERTEX_BUFFER_BINDING_GG"></span>


ドライバーは、新しい DP2 token、D3DDP2OP\_SETSTREAMSOURCE、およびそれに関連付けられている HAL データ構造体[**D3DHAL\_DP2SETSTREAMSOURCE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2setstreamsource)を通じて、特定のストリームに頂点バッファーをバインドすることを通知します。

 

 





