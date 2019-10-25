---
title: 圧縮テクスチャ サーフェスの作成
description: 圧縮テクスチャ サーフェスの作成
ms.assetid: 6d1cc079-642c-4662-ae72-c0362d8a5b2a
keywords:
- 圧縮されたテクスチャの描画 WDK DirectDraw、作成
- DirectDraw 圧縮テクスチャ WDK Windows 2000 ディスプレイ、作成
- 圧縮されたテクスチャサーフェス WDK DirectDraw、作成
- WDK DirectDraw、圧縮されたテクスチャを表面にします
- テクスチャ WDK DirectDraw、圧縮
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 84e3dba3c4d60583bdae6c035f8ffd6c12b6329d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839024"
---
# <a name="creating-the-compressed-texture-surface"></a>圧縮テクスチャ サーフェスの作成


## <span id="ddk_creating_the_compressed_texture_surface_gg"></span><span id="DDK_CREATING_THE_COMPRESSED_TEXTURE_SURFACE_GG"></span>


DirectDraw が画面を作成するようにドライバーに要求するたびに、ドライバーは、圧縮されたテクスチャサーフェイスを作成するかどうかを判断する必要があります。 これを確認するには、ドライバーは、作成されるサーフェイスの[**DDSURFACEDESC2**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550340(v=vs.85))構造体で、既に DirectDraw によって設定されている情報を確認する必要があります。 ドライバーには、次の検証手順が含まれている必要があります (任意の画面と同様)。

-   [**Ddscaps 構造体**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550286(v=vs.85))の**dwFlags**メンバーに、DDSCAPS\_テクスチャフラグがあるかどうかを確認します。

-   作成されているサーフェイスに対して、 [**ddpf**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddpixelformat) **使用する場合**は、ddpf\_FOURCC フラグを使用します。 このチェックは、次の**Dwfourcc**チェックの前に行われます。

-   作成されるサーフェイスの[**DDDXT の形式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddpixelformat)構造体の**dwfourcc**メンバー内のいずれかのコードがあるかどうかを確認します。

-   [**DDSURFACEDESC2**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550340(v=vs.85))構造体の width および height メンバー (**Dwwidth**と**dwHeight**) を確認します。 DirectDraw は、これらのメンバーを4ピクセルの倍数に設定します。

 

 





