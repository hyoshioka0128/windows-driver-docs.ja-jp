---
title: テクスチャのサポート
description: テクスチャのサポート
ms.assetid: 8ae4d4bf-9fef-4e5e-a88a-5cb93519c802
keywords:
- 図面ページ WDK DirectDraw、テクスチャを反転します。
- DirectDraw WDK Windows 2000 の表示、テクスチャの反転
- 反転 WDK DirectDraw、テクスチャをページします。
- WDK DirectDraw、テクスチャの反転
- WDK DirectDraw、テクスチャの反転
- 3D の表面 WDK DirectDraw を反転します。
- WDK の DirectDraw を画面の回転
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e03513d780c4ccdbcf70b84919c46266c84f7672
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553984"
---
# <a name="texture-support"></a>テクスチャのサポート


## <span id="ddk_texture_support_gg"></span><span id="DDK_TEXTURE_SUPPORT_GG"></span>


テクスチャ 3D 空間では、その他の任意の画面と同じ方法を反転します。 A*テクスチャ*を 3D の表面に bits を変換することを指定する設定 (テクスチャ マップ) を含むフラットなイメージだけです。 テクスチャは 3D の表面にマップできるし、テクスチャの反転 ページで、モーションをスムーズに表示できます。 フリップ レンダラー (スキャン ライン待機しています) などの読み取りが完了するまで待機します。 反転ドライバーでは、テクスチャをサポートする場合を認識し、適切に処理できない場合があります。 テクスチャの詳細については、[Direct3D テクスチャ管理](direct3d-texture-management.md)を参照してください。

 

 





