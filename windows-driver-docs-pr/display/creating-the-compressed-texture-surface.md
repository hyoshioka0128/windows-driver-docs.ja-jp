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
ms.openlocfilehash: 2dc2a9ebb7a7c9902efe56689e4e63244584b39e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370184"
---
# <a name="creating-the-compressed-texture-surface"></a>圧縮テクスチャ サーフェスの作成


## <span id="ddk_creating_the_compressed_texture_surface_gg"></span><span id="DDK_CREATING_THE_COMPRESSED_TEXTURE_SURFACE_GG"></span>


DirectDraw サーフェスを作成するドライバーを要求するたびに、ドライバーが圧縮テクスチャ サーフェスを作成する要求されているかどうかを決定する必要があります。 これを確認するドライバーがで DirectDraw が設定されていた情報を確認する必要があります、 [ **DDSURFACEDESC2** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550340(v=vs.85))画面の作成中の構造体。 ドライバーは、(任意の画面) と同様、次の検証手順を含める必要があります。

-   チェック、DDSCAPS\_テクスチャ フラグ、 **dwFlags**のメンバー、 [ **DDSCAPS** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550286(v=vs.85))構造体。

-   チェック、DDPF\_FOURCC フラグ、 **dwFlags**のメンバー、 [ **DDPIXELFORMAT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ddpixelformat)画面の作成中の構造。 このチェックは、次の前に出現する必要があります**dwFourCC**を確認します。

-   DXT コードのいずれかの確認、 **dwFourCC**のメンバー、 [ **DDPIXELFORMAT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ddpixelformat)画面の作成中の構造体。

-   幅と高さのメンバーをチェック (**dwWidth**と**dwHeight**) の[ **DDSURFACEDESC2** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550340(v=vs.85))構造体。 DirectDraw は 4 ピクセルの倍数にこれらのメンバーを設定します。

 

 





