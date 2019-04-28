---
title: ストリーム 0
description: ストリーム 0
ms.assetid: d6f0a625-c594-45b6-a229-b9c8a5275002
keywords:
- WDK の Windows 2000 の表示、複数のストリームの頂点の DirectX 8.0 リリース ノートします。
- 複数の頂点 WDK DirectX 8.0 をストリームします。
- 頂点 WDK DirectX 8.0 の複数のストリーム
- 0 個の WDK DirectX 8.0 をストリーム配信します。
- 頂点がゼロの WDK DirectX 8.0 をストリーム配信します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 837cfe8887973a692f4dbb54b155e43d6db52f1d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376001"
---
# <a name="stream-zero"></a>ストリーム 0


## <span id="ddk_stream_zero_gg"></span><span id="DDK_STREAM_ZERO_GG"></span>


頂点ストリーム 0 は、Direct3D の以前のバージョンでサポートされている唯一のストリームである他のストリームから異なる方法で扱われます。 柔軟な頂点の形式 (FVF) である、FVF フィールドは、0 以外の場合は、頂点バッファーは、0 のストリームにのみバインドできます。 ただし、わけではありません常に 0 のストリームにバインドされている頂点バッファーが柔軟な頂点形式であること。

Stream 0 も暗黙頂点ソース頂点シェーダーの現在のハンドル、特別な固定機能の頂点シェーダーのいずれかにできます。

 

 





