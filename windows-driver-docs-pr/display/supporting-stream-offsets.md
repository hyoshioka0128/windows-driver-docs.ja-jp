---
title: ストリーム オフセットのサポート
description: ストリーム オフセットのサポート
ms.assetid: 2c2ca906-8685-47f5-a2ca-855394b9674f
keywords:
- ストリームのオフセット WDK DirectX 9.0
- 頂点のストリームのオフセット WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3117ab6b50f90079661f901ab276180651f12e46
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361246"
---
# <a name="supporting-stream-offsets"></a>ストリーム オフセットのサポート


## <span id="ddk_supporting_stream_offsets_gg"></span><span id="DDK_SUPPORTING_STREAM_OFFSETS_GG"></span>


DirectX 9.0 バージョンのドライバーができるようにするためにサポートする必要がありますアプリケーションでは、1 つの頂点のデータ ストリームで複数の頂点の形式の頂点のデータを格納します。 アプリケーションに通知の頂点のデータ ストリームで指定することによって特定の形式の頂点のデータにある、ドライバー、*ストリーム オフセット*、(その頂点データの先頭に、バイト単位)。 ストリームのオフセットをサポートするために、ドライバーが、D3DDP2OP を処理する必要があります\_SETSTREAMSOURCE2 操作のコードでその[ **D3dDrawPrimitives2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)関数。 A [ **D3DHAL\_DP2SETSTREAMSOURCE2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_dp2setstreamsource2)構造体は、操作のコードに依存して、[コマンド ストリーム](command-stream.md)ストリームとのオフセットを指定するために使用頂点のデータがある場所です。

 

 





