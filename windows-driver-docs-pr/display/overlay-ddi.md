---
title: オーバーレイ DDI
description: オーバーレイ DDI
ms.assetid: c8f1cdd6-1beb-43bd-b96c-2eea3a51321e
keywords:
- DDI WDK Windows 7 のディスプレイにオーバーレイします。
- オーバーレイ DDI WDK Server 2008 R2 の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7053e1dc7e10045e4883f532c11483837f8ba59a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354704"
---
# <a name="overlay-ddi"></a>オーバーレイ DDI


このセクションでは、Windows 7 以降および Windows Server 2008 R2 以降のバージョンの Windows オペレーティング システムにのみ適用されます。

オーバーレイ DDI は拡張機能、 [Direct3D のバージョン 9 DDI](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/index)オーバーレイのサポートを確認します。 オーバーレイ DDI は、次のエントリ ポイントで構成されます。

-   D3DDDICAPS\_CHECKOVERLAYSUPPORT 値から、 [ **D3DDDICAPS\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ne-d3dumddi-_d3dddicaps_type)列挙は、ディスプレイ デバイスをサポートするかどうかを確認する Direct3D のランタイムによって使用されます、特定のオーバーレイします。 ランタイム設定 D3DDDICAPS\_で CHECKOVERLAYSUPPORT、**型**のメンバー、 [ **D3DDDIARG\_GETCAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)構造体、 *pData*のドライバーのパラメーター [ **GetCaps** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps)関数ランタイムが呼び出すときに指す**GetCaps**します。 また、ランタイムを設定、 **pInfo** D3DDDIARG のメンバー\_へのポインターに GETCAPS、 [ **DDICHECKOVERLAYSUPPORTINPUT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_ddicheckoverlaysupportinput)構造体をオーバーレイします。 ドライバーが D3DOVERLAYCAPS 構造体のメンバーを設定しには、この構造体へのポインターを返します、ドライバーは、オーバーレイをサポートする場合、 **pData**のメンバー **D3DDDIARG\_GETCAPS**します。 それ以外の場合、ドライバーが、オーバーレイをサポートしていない場合、ドライバーがへの呼び出しに失敗、 **GetCaps**か D3DDDIERR で関数を\_UNSUPPORTEDOVERLAYFORMAT または D3DDDIERR\_UNSUPPORTEDOVERLAY に応じてするかどうかのサポートの不足は、オーバーレイの形式に基づいていました。 D3DOVERLAYCAPS は DirectX SDK のドキュメントについて説明します。

    ドライバーのセット、 **MaxOverlayDisplayWidth**と**MaxOverlayDisplayHeight**を含む最終的なドライバーとハードウェアがある制限を示す D3DOVERLAYCAPS のメンバー(オーバーレイ データをストレッチ) 後のサイズをオーバーレイします。

    ドライバーの設定、D3DOVERLAYCAPS\_STRETCHX (0x00000040) と D3DOVERLAYCAPS\_STRETCHY (0x00000080) 機能のビットで、 **Cap**にオーバーレイ ハードウェアがあることを示す D3DOVERLAYCAPS のメンバー任意拡張とオーバーレイ データを圧縮できること。 ドライバーは GPU を伸縮オーバーレイをエミュレートするためにしないでください、オーバーレイのハードウェアは、拡大をサポートしている場合のみ、これらの上限を設定する必要があります。 オーバーヘッドが少ないがビデオの処理の一部として伸縮 GPU を実行するアプリケーションに必要なとドライバーの個別の実行を最後にエミュレートするために渡すよりも、合成フェーズ オーバーレイ伸縮します。

-   ドライバーから次のような新しいビット フィールド フラグを処理する必要があります、 [ **D3DDDI\_OVERLAYINFOFLAGS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddi_overlayinfoflags)構造体。 D3DDDI\_OVERLAYINFOFLAGS 構造が実行する操作をオーバーレイの種類を識別します。 D3DDDI\_OVERLAYINFOFLAGS 構造で指定されますが、**フラグ**のメンバー、 [ **D3DDDI\_OVERLAYINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddi_overlayinfo)への呼び出しで構造体ドライバーの[ **CreateOverlay** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createoverlay)または[ **UpdateOverlay** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_updateoverlay)関数。

    <span id="LimitedRGB"></span><span id="limitedrgb"></span><span id="LIMITEDRGB"></span>**LimitedRGB**  
    オーバーレイは、RGB の完全な範囲ではなく、限られた範囲 RGB です。 限られた範囲 RGB の 16時 16分: 16 は黒と 235:235:235 は白になるよう、RGB 範囲が圧縮されます。

    <span id="YCbCrBT709"></span><span id="ycbcrbt709"></span><span id="YCBCRBT709"></span>**YCbCrBT709**  
    オーバーレイを BT.709 で、高精細テレビ (HDTV) ではなく BT.601 を示します。

    <span id="YCbCrxvYCC"></span><span id="ycbcrxvycc"></span><span id="YCBCRXVYCC"></span>**YCbCrxvYCC**  
    オーバーレイは、従来の YCbCr ではなく YCbCr (xvYCC) に拡張されます。

-   32 ビットではなく、64 ビットの表示形式の場合 (D3DFMT を使用する場合など、Windows デスクトップ マネージャー (DWM)\_表示モードの A16B16G16R16F)、ランタイムでオーバーレイ colorkey の下位 32 ビットの配置、 **DstColorKeyLow**のメンバー、 [ **D3DDDI\_OVERLAYINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddi_overlayinfo)構造との上位 32 ビット、 **DstColorKeyHigh**のメンバーD3DDDI\_OVERLAYINFO します。

 

 





