---
title: DDI をオーバーレイします。
description: DDI をオーバーレイします。
ms.assetid: c8f1cdd6-1beb-43bd-b96c-2eea3a51321e
keywords:
- DDI WDK Windows 7 のディスプレイにオーバーレイします。
- オーバーレイ DDI WDK Server 2008 R2 の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ac22885f8e3375a72e7038eec2c6c37d96ca418
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553662"
---
# <a name="overlay-ddi"></a>DDI をオーバーレイします。


このセクションでは、Windows 7 以降および Windows Server 2008 R2 以降のバージョンの Windows オペレーティング システムにのみ適用されます。

オーバーレイ DDI は拡張機能、 [Direct3D のバージョン 9 DDI](https://msdn.microsoft.com/library/windows/hardware/ff552927)オーバーレイのサポートを確認します。 オーバーレイ DDI は、次のエントリ ポイントで構成されます。

-   D3DDDICAPS\_CHECKOVERLAYSUPPORT 値から、 [ **D3DDDICAPS\_型**](https://msdn.microsoft.com/library/windows/hardware/ff544132)列挙は、ディスプレイ デバイスをサポートするかどうかを確認する Direct3D のランタイムによって使用されます、特定のオーバーレイします。 ランタイム設定 D3DDDICAPS\_で CHECKOVERLAYSUPPORT、**型**のメンバー、 [ **D3DDDIARG\_GETCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff543148)構造体、 *pData*のドライバーのパラメーター [ **GetCaps** ](https://msdn.microsoft.com/library/windows/hardware/ff566762)関数ランタイムが呼び出すときに指す**GetCaps**します。 また、ランタイムを設定、 **pInfo** D3DDDIARG のメンバー\_へのポインターに GETCAPS、 [ **DDICHECKOVERLAYSUPPORTINPUT** ](https://msdn.microsoft.com/library/windows/hardware/ff549563)構造体をオーバーレイします。 ドライバーが D3DOVERLAYCAPS 構造体のメンバーを設定しには、この構造体へのポインターを返します、ドライバーは、オーバーレイをサポートする場合、 **pData**のメンバー **D3DDDIARG\_GETCAPS**します。 それ以外の場合、ドライバーが、オーバーレイをサポートしていない場合、ドライバーがへの呼び出しに失敗、 **GetCaps**か D3DDDIERR で関数を\_UNSUPPORTEDOVERLAYFORMAT または D3DDDIERR\_UNSUPPORTEDOVERLAY に応じてするかどうかのサポートの不足は、オーバーレイの形式に基づいていました。 D3DOVERLAYCAPS は DirectX SDK のドキュメントについて説明します。

    ドライバーのセット、 **MaxOverlayDisplayWidth**と**MaxOverlayDisplayHeight**を含む最終的なドライバーとハードウェアがある制限を示す D3DOVERLAYCAPS のメンバー(オーバーレイ データをストレッチ) 後のサイズをオーバーレイします。

    ドライバーの設定、D3DOVERLAYCAPS\_STRETCHX (0x00000040) と D3DOVERLAYCAPS\_STRETCHY (0x00000080) 機能のビットで、 **Cap**にオーバーレイ ハードウェアがあることを示す D3DOVERLAYCAPS のメンバー任意拡張とオーバーレイ データを圧縮できること。 ドライバーは GPU を伸縮オーバーレイをエミュレートするためにしないでください、オーバーレイのハードウェアは、拡大をサポートしている場合のみ、これらの上限を設定する必要があります。 オーバーヘッドが少ないがビデオの処理の一部として伸縮 GPU を実行するアプリケーションに必要なとドライバーの個別の実行を最後にエミュレートするために渡すよりも、合成フェーズ オーバーレイ伸縮します。

-   ドライバーから次のような新しいビット フィールド フラグを処理する必要があります、 [ **D3DDDI\_OVERLAYINFOFLAGS** ](https://msdn.microsoft.com/library/windows/hardware/ff544626)構造体。 D3DDDI\_OVERLAYINFOFLAGS 構造が実行する操作をオーバーレイの種類を識別します。 D3DDDI\_OVERLAYINFOFLAGS 構造で指定されますが、**フラグ**のメンバー、 [ **D3DDDI\_OVERLAYINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff544621)への呼び出しで構造体ドライバーの[ **CreateOverlay** ](https://msdn.microsoft.com/library/windows/hardware/ff540662)または[ **UpdateOverlay** ](https://msdn.microsoft.com/library/windows/hardware/ff570107)関数。

    <span id="LimitedRGB"></span><span id="limitedrgb"></span><span id="LIMITEDRGB"></span>**LimitedRGB**  
    オーバーレイは、RGB の完全な範囲ではなく、限られた範囲 RGB です。 限られた範囲 RGB の 16時 16分: 16 は黒と 235:235:235 は白になるよう、RGB 範囲が圧縮されます。

    <span id="YCbCrBT709"></span><span id="ycbcrbt709"></span><span id="YCBCRBT709"></span>**YCbCrBT709**  
    オーバーレイを BT.709 で、高精細テレビ (HDTV) ではなく BT.601 を示します。

    <span id="YCbCrxvYCC"></span><span id="ycbcrxvycc"></span><span id="YCBCRXVYCC"></span>**YCbCrxvYCC**  
    オーバーレイは、従来の YCbCr ではなく YCbCr (xvYCC) に拡張されます。

-   32 ビットではなく、64 ビットの表示形式の場合 (D3DFMT を使用する場合など、Windows デスクトップ マネージャー (DWM)\_表示モードの A16B16G16R16F)、ランタイムでオーバーレイ colorkey の下位 32 ビットの配置、 **DstColorKeyLow**のメンバー、 [ **D3DDDI\_OVERLAYINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff544621)構造との上位 32 ビット、 **DstColorKeyHigh**のメンバーD3DDDI\_OVERLAYINFO します。

 

 





