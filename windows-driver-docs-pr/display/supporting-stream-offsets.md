---
title: ストリーム オフセットのサポート
description: ストリーム オフセットのサポート
ms.assetid: 2c2ca906-8685-47f5-a2ca-855394b9674f
keywords:
- ストリームオフセット WDK DirectX 9.0
- 頂点ストリームオフセット WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a48186483c0c28784170af69d29b73d5696277e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829382"
---
# <a name="supporting-stream-offsets"></a>ストリーム オフセットのサポート


## <span id="ddk_supporting_stream_offsets_gg"></span><span id="DDK_SUPPORTING_STREAM_OFFSETS_GG"></span>


DirectX 9.0 バージョンのドライバーでは、複数の頂点形式の頂点データを1つの頂点データストリームに格納することをアプリケーションにサポートする必要があります。 アプリケーションは、特定の形式の頂点*データを頂点*データストリームに格納する場所を、その頂点データの先頭にバイト単位で指定することによって、ドライバーに通知します。 ストリームオフセットをサポートするには、ドライバーで[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)関数の D3DDP2OP\_SETSTREAMSOURCE2 operation コードを処理する必要があります。 [**D3DHAL\_DP2SETSTREAMSOURCE2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2setstreamsource2)構造体は、[コマンドストリーム](command-stream.md)内の操作コードに従います。ストリームと、頂点データが配置される位置のオフセットを指定するために使用されます。

 

 





