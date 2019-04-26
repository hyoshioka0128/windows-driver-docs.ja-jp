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
ms.openlocfilehash: 8ca8485f65e7c74ff0ef3e4c959dbaac8bfc9a29
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345534"
---
# <a name="notification-of-stream-and-vertex-buffer-binding"></a>ストリーム バッファーと頂点バッファーのバインドの通知


## <span id="ddk_notification_of_stream_vertex_buffer_binding_gg"></span><span id="DDK_NOTIFICATION_OF_STREAM_VERTEX_BUFFER_BINDING_GG"></span>


ドライバーは、次のように新しい DP2 トークン D3DDP2OP で特定のストリームを頂点バッファーのバインドの通知\_SETSTREAMSOURCE、およびその関連付けられている HAL データ構造[ **D3DHAL\_DP2SETSTREAMSOURCE**](https://msdn.microsoft.com/library/windows/hardware/ff545798).

 

 





