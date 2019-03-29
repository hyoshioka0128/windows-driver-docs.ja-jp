---
title: 複数頂点ストリーム機能のレポート
description: 複数頂点ストリーム機能のレポート
ms.assetid: 61441576-0e5d-4c6d-9e36-dcd8c59c8db0
keywords:
- WDK の Windows 2000 の表示、複数のストリームの頂点の DirectX 8.0 リリース ノートします。
- 複数の頂点 WDK DirectX 8.0 をストリームします。
- 頂点 WDK DirectX 8.0 の複数のストリーム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d229a5b39a2e40b82d048c0f2b60c27349e3317
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574771"
---
# <a name="reporting-multiple-vertex-stream-capability"></a>複数頂点ストリーム機能のレポート


## <span id="ddk_reporting_multiple_vertex_stream_capability_gg"></span><span id="DDK_REPORTING_MULTIPLE_VERTEX_STREAM_CAPABILITY_GG"></span>


ドライバーの値を設定して、複数の頂点のストリームをサポートする機能の報告、 **MaxStreams** D3DCAPS8 構造体のフィールド。 複数の頂点のストリームをサポートしているドライバーには、1 より大きい値を指定する必要があります。 複数の頂点のストリームをサポートしていない DX8 レベル ドライバーを設定する必要があります**MaxStreams**いずれかにします。 このフィールドに 0 の値を指定する必要があります DX8 レベルのドライバーにはありません。 ドライバーを設定する必要がありますも、 **MaxStreamStride**フィールド頂点ストリーム内の要素の頂点間のバイト単位で最大サポートされている stride をします。

 

 





