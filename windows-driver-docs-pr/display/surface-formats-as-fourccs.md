---
title: FOURCC としてのサーフェスの形式
description: FOURCC としてのサーフェスの形式
ms.assetid: 947b73c9-3f1d-485e-9966-815b40a06342
keywords:
- テクスチャ形式の一覧が DirectX 8.0 リリース ノート WDK Windows 2000 の表示
- テクスチャ形式には、WDK の DirectX 8.0 が一覧表示されます。
- DPIXELFORMAT
- 画面は WDK DirectX 8.0 を書式設定します。
- Fourcc
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c25c9a13bcb7b2c48f75320b5b39f047f528b3fa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577797"
---
# <a name="surface-formats-as-fourccs"></a>FOURCC としてのサーフェスの形式


## <span id="ddk_surface_formats_as_fourccs_gg"></span><span id="DDK_SURFACE_FORMATS_AS_FOURCCS_GG"></span>


DirectX 8.0、D3DFMT により定義された新しい surface 形式の 3 つ\_Q8W8V8U8、D3DFMT\_V16U16 と D3DFMT\_W11V11U10、としてドライバーに渡される*Fourcc*します。 つまり、さまざまなビットの深さとマスク フィールド、 [ **DDPIXELFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff550274)データ構造が初期化されていないと、その値が定義されていません。 そのため、これら 3 つの形式を処理するドライバーがビット数に依存する必要がありますまたはマスク ピクセル形式にする必要がありますが、必要に応じて、これらを計算します。 たとえばの画面の声の高さを計算するときにこれらのいずれかの型、 **dwRGBBitCount**ピクセル形式のフィールドを使用しない必要があります。 他のすべての YUV、DXT および IHV の特定の拡張子形式がドライバーに渡されるときに、レガシ DDPIXELFORMAT 表現にマップされている以外の形式であり、そのため、有効ピクセル形式とマスク ピクセル形式のデータ構造で。

 

 





