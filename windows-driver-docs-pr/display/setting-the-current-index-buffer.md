---
title: 現在のインデックス バッファーの設定
description: 現在のインデックス バッファーの設定
ms.assetid: 4d190ce1-56a0-4445-9a68-6a24f3a9aee4
keywords:
- DirectX 8.0 リリース ノートには、Windows 2000 の WDK 表示インデックス バッファー
- インデックス バッファー WDK Directx 8.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dbd3afef68b667f8fc5ecc1ce128295f51fb8908
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390439"
---
# <a name="setting-the-current-index-buffer"></a>現在のインデックス バッファーの設定


## <span id="ddk_setting_the_current_index_buffer_gg"></span><span id="DDK_SETTING_THE_CURRENT_INDEX_BUFFER_GG"></span>


頂点のデータと同様プリミティブを描画することによって使用されるインデックス バッファーは、プリミティブ型で、ドライバーに渡されるデータの一部ではなくなりましたが、ドライバーの状態はではなく、します。 現在インデックス バッファーは、次のように新しい DP2 トークン D3DDP2OP 設定\_SETINDICES します。 このトークンでは、新しいインデックス バッファーが設定されているか、現在のインデックス バッファーをクリアするまでは、インデックス付きのプリミティブを描画するときに使用する現在のインデックス バッファーとして指定されたハンドル、インデックス バッファーが確立されている (DP2 トークン データで 0、インデックス バッファー ハンドルを指定します)。

 

 





