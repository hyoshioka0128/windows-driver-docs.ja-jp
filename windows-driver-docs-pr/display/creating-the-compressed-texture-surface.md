---
title: 圧縮テクスチャ サーフェスの作成
description: 圧縮テクスチャ サーフェスの作成
ms.assetid: 6d1cc079-642c-4662-ae72-c0362d8a5b2a
keywords:
- 圧縮されたテクスチャ WDK DirectDraw を描画、作成します。
- DirectDraw 圧縮テクスチャ WDK Windows 2000 では、表示を作成します。
- 圧縮されたテクスチャ サーフェスの WDK の DirectDraw を作成します。
- WDK DirectDraw、圧縮されたテクスチャを表示します。
- 圧縮テクスチャ WDK DirectDraw、
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d81b763acf3677e1062855602c7ff9d9584ff60
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387231"
---
# <a name="creating-the-compressed-texture-surface"></a>圧縮テクスチャ サーフェスの作成


## <span id="ddk_creating_the_compressed_texture_surface_gg"></span><span id="DDK_CREATING_THE_COMPRESSED_TEXTURE_SURFACE_GG"></span>


DirectDraw サーフェスを作成するドライバーを要求するたびに、ドライバーが圧縮テクスチャ サーフェスを作成する要求されているかどうかを決定する必要があります。 これを確認するドライバーがで DirectDraw が設定されていた情報を確認する必要があります、 [ **DDSURFACEDESC2** ](https://msdn.microsoft.com/library/windows/hardware/ff550340)画面の作成中の構造体。 ドライバーは、(任意の画面) と同様、次の検証手順を含める必要があります。

-   チェック、DDSCAPS\_テクスチャ フラグ、 **dwFlags**のメンバー、 [ **DDSCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff550286)構造体。

-   チェック、DDPF\_FOURCC フラグ、 **dwFlags**のメンバー、 [ **DDPIXELFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff550274)画面の作成中の構造。 このチェックは、次の前に出現する必要があります**dwFourCC**を確認します。

-   DXT コードのいずれかの確認、 **dwFourCC**のメンバー、 [ **DDPIXELFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff550274)画面の作成中の構造体。

-   幅と高さのメンバーをチェック (**dwWidth**と**dwHeight**) の[ **DDSURFACEDESC2** ](https://msdn.microsoft.com/library/windows/hardware/ff550340)構造体。 DirectDraw は 4 ピクセルの倍数にこれらのメンバーを設定します。

 

 





