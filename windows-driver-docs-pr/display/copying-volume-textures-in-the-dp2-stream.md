---
title: DP2 ストリームでのボリューム テクスチャのコピー
description: DP2 ストリームでのボリューム テクスチャのコピー
ms.assetid: c7f982d8-d35b-4462-a0cf-49dfb82860f8
keywords:
- WDK DirectX 8.0 のテクスチャ
- Windows 2000 の WDK の表示、ボリュームのテクスチャの DirectX 8.0 リリース ノートします。
- ボリューム テクスチャ WDK DirectX 8.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b225f03106e802d10706dbeb3ab7e813c4d2d2b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390019"
---
# <a name="copying-volume-textures-in-the-dp2-stream"></a>DP2 ストリームでのボリューム テクスチャのコピー


## <span id="ddk_copying_volume_textures_in_the_dp2_stream_gg"></span><span id="DDK_COPYING_VOLUME_TEXTURES_IN_THE_DP2_STREAM_GG"></span>


新しい DP2 トークン、D3DDP2OP\_VOLUMEBLT が最適なコピーとボリュームのテクスチャの更新をサポートするために追加されました。 このトークンは、既存の D3DDP2OP によく似ています\_TEXBLT コピーおよびテクスチャの更新が単純な四角形ではなく subvolume (ボックス) のコピーをサポートするために拡張されています。

 

 





