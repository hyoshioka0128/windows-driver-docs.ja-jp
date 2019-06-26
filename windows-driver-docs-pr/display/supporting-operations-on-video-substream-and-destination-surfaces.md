---
title: ビデオ サブストリームおよび宛先サーフェスに対する操作
description: VMR 以降では、Microsoft Windows Server 2003 SP1 および Windows XP SP2 とビデオのサブストリームと宛先表面で特定の操作を実行することが後である必要があります。
ms.assetid: ad0214b9-5d75-455f-8748-ff7c5a3d89db
keywords:
- DeinterlaceBltEx、宛先表面
- DeinterlaceBltEx、サブストリーム サーフェス
- 移行先サーフェスの WDK DirectX VA
- サブストリームのサーフェス WDK DirectX VA
- いっぱいになる宛先表面 WDK DirectX VA を色します。
- 色の塗りつぶしサブストリーム サーフェス WDK DirectX VA
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: fbadc4d44feed8cc8638c46ff7aadc4610c82a1e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380532"
---
# <a name="operations-on-video-substream-and-destination-surfaces"></a>ビデオ サブストリームおよび宛先サーフェスに対する操作


## <span id="ddk_supporting_operations_on_video_substream_and_destination_surfaces_"></span><span id="DDK_SUPPORTING_OPERATIONS_ON_VIDEO_SUBSTREAM_AND_DESTINATION_SURFACES_"></span>


**このセクションでは、Windows Server 2003 SP1 以降、および Windows XP SP2 以降にのみ適用されます。**

VMR 以降では、Microsoft Windows Server 2003 SP1 および Windows XP SP2 とビデオのサブストリームと宛先表面で特定の操作を実行することが後である必要があります。

### <a name="span-idoperationsonvideosubstreamsurfacesspanspan-idoperationsonvideosubstreamsurfacesspanspan-idoperationsonvideosubstreamsurfacesspanoperations-on-video-substream-surfaces"></a><span id="Operations_on_Video_Substream_Surfaces"></span><span id="operations_on_video_substream_surfaces"></span><span id="OPERATIONS_ON_VIDEO_SUBSTREAM_SURFACES"></span>ビデオ サブストリーム サーフェスでの操作

ビデオのサブストリームの業務に加えてサーフェスをドライバーの[ **DeinterlaceBltEx** ](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlacebltex)と[ **DeinterlaceBlt** ](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlaceblt)関数の実行、ドライバーは、次の操作をサポートする必要があります。

<span id="Color_Filling_Substream_Surfaces"></span><span id="color_filling_substream_surfaces"></span><span id="COLOR_FILLING_SUBSTREAM_SURFACES"></span>**色の塗りつぶしサブストリーム サーフェス**  
VMR とその他の Microsoft DirectShow のコンポーネントはビデオ サブストリームの表面を透明な黒などの既知の初期カラー値を入力できる必要があります。 ドライバーがへの呼び出しをサポートするために、その[ *DdBlt* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_blt) 、DDBLT を使用してコールバック関数\_COLORFILL フラグがビデオ サブストリーム サーフェスがビット ブロックのターゲットは転送 (blt)。

AYUV のサーフェスでビデオ サブストリーム*FOURCC*形式、VMR で透明な黒の AYUV 色を指定します、 **dwFillColor** DDBLTFX 構造体のメンバー。 ドライバーの受信で DDBLTFX、 **bltFX** 、DD のメンバー\_BLTDATA 構造ときにその*DdBlt*関数が呼び出されます。 DDBLTFX 構造については、Windows SDK のドキュメントを参照してください。

透明な黒の色を AYUV はよう設定します。

```cpp
DXVA_AYUVsample2 clr; 
clr.bCrValue = 0x80;
clr.bCbValue = 0x80;
clr.bY_Value = 0x10;
clr.bSampleAlpha8 = 0x00;
DWORD dwFillColor = *(DWORD*)&clr;
```

AI44 または IA44 形式、内の値の下位バイトのサーフェスでビデオ サブストリーム、 **dwFillColor**メンバーは、ドライバーが、画面の塗りつぶしに使用する色の値を示します。 通常、色の値には 0 です。

<span id="Copying_Contents_to_Substream_Surfaces"></span><span id="copying_contents_to_substream_surfaces"></span><span id="COPYING_CONTENTS_TO_SUBSTREAM_SURFACES"></span>**内容をサブストリーム サーフェスにコピーします。**  
閉じられた Line21 キャプション デコーダーと文字放送デコーダーは、キャッシュされている文字グリフのデータ系列を含むソース ビデオ サブストリーム サーフェスを作成します。 ドライバーは、ビデオ サブストリームの画面にグリフのキャッシュから適切な文字をコピーして各フレームの出力を生成する必要があります。 VMR を送信しますビデオ サブストリーム surface ドライバーの[ **DeinterlaceBltEx** ](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlacebltex)関数。

そのため、ドライバーの[ *DdBlt* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_blt)関数が同じ FOURCC 形式のビデオ サブストリーム画面に FOURCC サーフェスのコピーをサポートする必要があります。

ドライバーは、DDCAPS2 を設定して、コピーの FOURCC 形式をサポートしていることを示す必要があります\_COPYFOURCC フラグ、 **dwCaps2**のメンバー、 [ **DDCORECAPS** ](https://docs.microsoft.com/windows/desktop/api/ddrawi/ns-ddrawi-_ddcorecaps)構造体。 ドライバーで DDCORECAPS 構造体を指定する、 **ddCaps**のメンバー、 [ **DD\_HALINFO** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_halinfo)構造体。 DD\_HALINFO がドライバーのによって返される[ **DrvGetDirectDrawInfo** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgetdirectdrawinfo)関数。

FOURCC ビデオ サブストリームのサーフェスのコピー操作では、ドライバーは拡大または色空間の変換操作を実行しないでください。

### <a name="span-idoperationsondestinationsurfacesspanspan-idoperationsondestinationsurfacesspanspan-idoperationsondestinationsurfacesspanoperations-on-destination-surfaces"></a><span id="Operations_on_Destination_Surfaces"></span><span id="operations_on_destination_surfaces"></span><span id="OPERATIONS_ON_DESTINATION_SURFACES"></span>宛先表面での操作

ドライバーは、ドライバーのために使用される変換先の画面で、次の操作をサポートする必要があります[ **DeinterlaceBltEx** ](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlacebltex)関数。

<span id="Color_Filling_the_Destination_Surface"></span><span id="color_filling_the_destination_surface"></span><span id="COLOR_FILLING_THE_DESTINATION_SURFACE"></span>**入力宛先表面の色**  
VMR YUV 黒、ドライバー、必要がありますが不透明に転送先のサーフェスを初期化する必要がありますのでもサポートへの呼び出し、 [ *DdBlt* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_blt) 、DDBLT を使用してコールバック関数\_COLORFILL フラグ where、ビット ブロック転送のターゲットは、宛先表面です。 VMR で不透明な黒の色を指定する、 **dwFillColor** DDBLTFX 構造体のメンバー。 ドライバーで DDBLTFX 構造が受信、 **bltFX** 、DD のメンバー\_BLTDATA 構造ときにその*DdBlt*が呼び出されます。

VMR はサーフェイスのタイプをパックされた YUV、DWORD の塗りつぶしの色を不透明な黒の適切なバイト パターンを設定します。 YUY2 画面 0x80108010 は不透明な黒の塗りつぶしの色 DWORD です。

平面のサーフェイスのタイプの VMR ように設定します不透明な黒の AYUV 色。

```cpp
DXVA_AYUVsample2 clr; 
clr.bCrValue = 0x80;
clr.bCbValue = 0x80;
clr.bY_Value = 0x10;
clr.bSampleAlpha8 = 0xFF;
DWORD dwFillColor = *(DWORD*)&clr;
```

ドライバーでは、YUV サーフェイスの各平面に正しいピクセル値が書き込まれることを確認してください。

<span id="Stretching_the_Destination_Surface"></span><span id="stretching_the_destination_surface"></span><span id="STRETCHING_THE_DESTINATION_SURFACE"></span>**宛先表面を拡大**  
ドライバーでは、色空間変換と拡張操作を結合するビット ブロック転送のソースの画面として使用される宛先表面もサポートする必要があります。 詳細については、次を参照してください。 [Stretch Blit 操作のサポート](supporting-stretch-blit-operations.md)します。

<span id="Copying_Contents_from_the_Destination_Surface"></span><span id="copying_contents_from_the_destination_surface"></span><span id="COPYING_CONTENTS_FROM_THE_DESTINATION_SURFACE"></span>**転送先のサーフェスからの内容のコピー**  
ドライバーの*DdBlt*関数が同じ FOURCC 形式のサーフェイスに FOURCC 宛先表面のコピーをサポートする必要があります。 転送先のサーフェイスは、コピー操作でソース画面として使用されます。 ドライバーは、DDCAPS2 を設定して、コピーの FOURCC 形式をサポートしていることを示す必要があります\_COPYFOURCC フラグ。

ビット ブロック転送操作の宛先表面には、プライマリの画面または Direct3D テクスチャを指定できます。

 

 





