---
title: オーバーレイ DDI
description: オーバーレイ DDI
ms.assetid: c8f1cdd6-1beb-43bd-b96c-2eea3a51321e
keywords:
- オーバーレイ DDI WDK Windows 7 ディスプレイ
- オーバーレイ DDI WDK サーバー 2008 R2 ディスプレイ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7276ccced91896f2dc537ec616955f38b148e128
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826068"
---
# <a name="overlay-ddi"></a>オーバーレイ DDI


このセクションは、windows 7 以降、および windows Server 2008 R2 以降のバージョンの Windows オペレーティングシステムにのみ適用されます。

オーバーレイ DDI は、オーバーレイサポートを確認するための[Direct3D バージョン 9 DDI](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/index)の拡張機能です。 オーバーレイ DDI は、次のエントリポイントで構成されています。

-   [**D3DDDICAPS\_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-_d3dddicaps_type)列挙の D3DDDICAPS\_CHECKOVERLAYSUPPORT 値は、ディスプレイデバイスが特定のオーバーレイをサポートするかどうかを確認するために、Direct3D ランタイムによって使用されます。 ランタイムは、ランタイムが**getcaps**を呼び出すときに、ドライバーの[**Getcaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps)関数の*pData*パラメーターが指す[**D3DDDIARG\_getcaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)構造体の**Type**メンバーで D3DDDICAPS\_CHECKOVERLAYSUPPORT を設定します。 また、ランタイムは、D3DDDIARG\_GETCAPS の**pInfo**メンバーに、オーバーレイを記述する[**DDICHECKOVERLAYSUPPORTINPUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_ddicheckoverlaysupportinput)構造体へのポインターを設定します。 ドライバーがオーバーレイをサポートしている場合、ドライバーは D3DOVERLAYCAPS 構造体のメンバーを設定し、 **D3DDDIARG\_GETCAPS**の**pData**メンバー内のこの構造体へのポインターを返します。 そうしないと、ドライバーがオーバーレイをサポートしていない場合、ドライバーは、サポートがないかどうかに応じて、D3DDDIERR\_UNSUPPORTEDOVERLAYFORMAT または D3DDDIERR\_UNSUPPORTEDOVERLAY で**Getcaps**関数への呼び出しに失敗します。オーバーレイ形式に基づいています。 D3DOVERLAYCAPS については、DirectX SDK のドキュメントを参照してください。

    ドライバーは、D3DOVERLAYCAPS の**MaxOverlayDisplayWidth**メンバーと**MaxOverlayDisplayHeight**メンバーを設定して、最終的なオーバーレイサイズ (オーバーレイデータを拡大した後) を含む、ドライバーとハードウェアに関する制限を示します。).

    ドライバーは D3DOVERLAYCAPS の**Caps**メンバーで D3DOVERLAYCAPS\_STRETCHX (0x00000040) および D3DOVERLAYCAPS\_可変幅 (0x00000040) の機能ビットを設定して、オーバーレイハードウェアを任意に拡張できることを示します。また、オーバーレイデータを圧縮します。 ドライバーは、GPU を使用したオーバーレイの拡大をエミュレートすることはできません。オーバーレイハードウェアが拡大をサポートしている場合にのみ、これらのキャップを設定してください。 通常、アプリケーションでは、ビデオ処理および合成フェーズの一環として GPU 拡張を実行するために、アプリケーションで GPU 拡張を実行する必要があります。

-   ドライバーは、 [**D3DDDI\_OVERLAYINFOFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddi_overlayinfoflags)構造体から、次の新しいビットフィールドフラグを処理する必要があります。 D3DDDI\_OVERLAYINFOFLAGS 構造体は、実行するオーバーレイ操作の種類を識別します。 D3DDDI\_OVERLAYINFOFLAGS 構造体は、ドライバーの[**createoverlay**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createoverlay)関数または[**updateoverlay**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_updateoverlay)関数の呼び出しで[**D3DDDI\_OVERLAYINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddi_overlayinfo)構造体の**Flags**メンバーに指定されます。

    <span id="LimitedRGB"></span><span id="limitedrgb"></span><span id="LIMITEDRGB"></span>**LimitedRGB**  
    オーバーレイは、全範囲の RGB ではなく、範囲の RGB に限定されます。 限られた範囲の RGB では、RGB の範囲が圧縮されるので、16:16:16 は黒、235:235:235 は白になります。

    <span id="YCbCrBT709"></span><span id="ycbcrbt709"></span><span id="YCBCRBT709"></span>**YCbCrBT709**  
    オーバーレイは709であり、BT ではなく高解像度テレビ (HDTV) を示します。

    <span id="YCbCrxvYCC"></span><span id="ycbcrxvycc"></span><span id="YCBCRXVYCC"></span>**YCbCrxvYCC**  
    オーバーレイは、従来の YCbCr ではなく、拡張された YCbCr (xvYCC) です。

-   表示形式が32ビットではなく64ビットである場合 (たとえば、デスクトップ Windows マネージャー (DWM) が D3DFMT\_A16B16G16R16F を表示モードで使用する場合)、ランタイムは、オーバーレイ colorkey の下位32ビットを**Dstcolorkeylow**メンバーに配置します。[**D3DDDI\_OVERLAYINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddi_overlayinfo)構造体と D3DDDI\_OVERLAYINFO の**Dstcolorkeyhigh**メンバーの上位32ビット。

 

 





