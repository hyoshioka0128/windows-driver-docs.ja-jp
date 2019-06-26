---
title: Direct3D ドライバーの初期化
description: Direct3D ドライバーの初期化
ms.assetid: ef37a570-a94e-4021-b84f-4436aa454ac5
keywords:
- Direct3D のドライバーの初期化
- Direct3D WDK Windows 2000 の表示、初期化
- DrvGetDirectDrawInfo
- DdGetDriverInfo
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a02056b4feddb290f8c6106d281e8af9f6d71971
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384869"
---
# <a name="direct3d-driver-initialization"></a>Direct3D ドライバーの初期化


## <span id="ddk_direct3d_driver_initialization_gg"></span><span id="DDK_DIRECT3D_DRIVER_INITIALIZATION_GG"></span>


ときに、ドライバーの[ **DrvGetDirectDrawInfo** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgetdirectdrawinfo)関数は、DirectDraw サポートを初期化するために Microsoft DirectDraw ランタイムによって呼び出される、ドライバーは、マイクロソフトの Direct3D を示すためには、次を行う必要があります機能:

-   設定、DDCAPS\_で 3D のフラグ、 **ddCaps.dwCaps**のメンバー、 [ **DD\_HALINFO** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_halinfo)構造体をドライバーのハードウェアが 3D であることを示す高速化します。

-   設定、DDSCAPS\_*Xxx*のフラグ、 **ddCaps.ddsCaps** 、DD のメンバー\_ドライバーのビデオ メモリ領域の 3D 機能を記述する HALINFO 構造体。 フラグは、次の表に一覧表示されます。

    <table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">Flag</th>
    <th align="left">意味</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><p>DDSCAPS_3DDEVICE</p></td>
    <td align="left"><p>ドライバーの表面を 3D レンダリング先として使用できることを示します。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>DDSCAPS_TEXTURE</p></td>
    <td align="left"><p>ドライバーの表面を 3D テクスチャ マッピングに使用できることを示します。</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>DDSCAPS_ZBUFFER</p></td>
    <td align="left"><p>ドライバーの表面を Z バッファーとして使用できることを示します。</p></td>
    </tr>
    </tbody>
    </table>

     

<!-- -->

-   設定、 **GetDriverInfo**のメンバー、 [ **DD\_HALINFO** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_halinfo)構造体をポイントして、ドライバーの[ **DdGetDriverInfo** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverinfo)コールバック。 ドライバーは、DDHALINFO を設定する必要がありますも\_GETDRIVERINFOSET フラグ、 **dwFlags** 、DD のメンバー\_HALINFO 構造が実装されていることを示す、 **DdGetDriverInfo**コールバック。

-   割り当ておよびのメンバーの初期化、 [ **D3DHAL\_コールバック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_callbacks)でこの構造体を返す構造体であり、 **lpD3DHALCallbacks** DD のメンバー\_HALINFO 構造体。

-   割り当ておよびのメンバーの初期化、 [ **D3DHAL\_GLOBALDRIVERDATA** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_globaldriverdata)でこの構造体を返す構造体であり、 **lpD3DGlobalDriverData**メンバーDD の\_HALINFO 構造体。

ドライバーが Microsoft DirectX 7.0 で対応可能であることを示す、以下を実行します。

-   含める、D3DDEVCAPS\_DRAWPRIMITIVES2EX フラグ、 **dwDevCaps**のメンバー、 [ **D3DDEVICEDESC\_V1** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3ddevicedesc_v1)に報告する構造体マイクロソフトの Direct3D のドライバーの初期化中に

-   GUID に対応\_で Miscellaneous2Callbacks GUID **DdGetDriverInfo**コールバックを設定して、 **GetDriverState**、 **CreateSurfaceEx**、および**DestroyDDLocal**のメンバー、 [ **DD\_MISCELLANEOUS2CALLBACKS** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_miscellaneous2callbacks)構造体。 Direct3D のドライバーとの or 演算の適切なコールバックをポイントするこれらの設定は、 **dwFlags** 、DDHAL を持つメンバー\_MISC2CB32\_CREATESURFACEEX、DDHAL\_MISC2CB32\_GETDRIVERSTATE、および DDHAL\_MISC2CB32\_DESTROYDDLOCAL ビットをそれぞれします。

後[ **DrvGetDirectDrawInfo** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgetdirectdrawinfo)返します、GDI の呼び出し、ドライバーの[ **DdGetDriverInfo** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverinfo)コールバック異なる Guid を複数回ドライバーの初期化を完了します。 **DdGetDriverInfo** Direct3D をサポートする次の Guid にコールバックが応答する必要があります。

<span id="GUID_D3DCallbacks3"></span><span id="guid_d3dcallbacks3"></span><span id="GUID_D3DCALLBACKS3"></span>GUID\_D3DCallbacks3  
ドライバーの割り当てし、のメンバーを初期化する必要があります、 [ **D3DHAL\_CALLBACKS3** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_callbacks3)でこの構造体を返す構造体であり、 **lpvData**のメンバー、[ **DD\_GETDRIVERINFODATA** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_getdriverinfodata)構造体。

<span id="GUID_Miscellaneous2Callbacks"></span><span id="guid_miscellaneous2callbacks"></span><span id="GUID_MISCELLANEOUS2CALLBACKS"></span>GUID\_Miscellaneous2Callbacks  
ドライバーの割り当てし、のメンバーを初期化する必要があります、 [ **DD\_MISCELLANEOUS2CALLBACKS** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_miscellaneous2callbacks)でこの構造体を返す構造体であり、 **lpvData**メンバー、DD の\_GETDRIVERINFODATA 構造体。

<span id="GUID_D3DExtendedCaps"></span><span id="guid_d3dextendedcaps"></span><span id="GUID_D3DEXTENDEDCAPS"></span>GUID\_D3DExtendedCaps  
ドライバーの割り当てし、の適切なメンバーを初期化する必要があります、 [ **D3DHAL\_D3DEXTENDEDCAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_d3dextendedcaps)でこの構造体を返す構造体であり、 **lpvData**、DD のメンバー\_GETDRIVERINFODATA 構造体。

<span id="GUID_ZPixelFormats"></span><span id="guid_zpixelformats"></span><span id="GUID_ZPIXELFORMATS"></span>GUID\_ZPixelFormats  
ドライバーの割り当てし、の適切なメンバーを初期化する必要があります、 [ **DDPIXELFORMAT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ddpixelformat)をドライバーがサポートしでこれらの構造体を返すすべての Z バッファー形式の構造、 **lpvData** 、DD のメンバー\_GETDRIVERINFODATA 構造体。 ドライバーは、D3DDP2OP をサポートしている場合にこの GUID に対応する必要が\_の実装でクリア操作コード[ **D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)します。

<span id="GUID_D3DParseUnknownCommandCallback"></span><span id="guid_d3dparseunknowncommandcallback"></span><span id="GUID_D3DPARSEUNKNOWNCOMMANDCALLBACK"></span>GUID\_D3DParseUnknownCommandCallback  
ドライバーは、Direct3D ランタイムへのポインターを格納する必要があります**D3DParseUnknownCommand**コールバック。 ポインターがドライバーに渡される、 **lpvData** 、DD のメンバー\_GETDRIVERINFODATA 構造体。 ドライバーの[ **D3dDrawPrimitives2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)コールバックの呼び出し、 **D3DParseUnknownCommand**ドライバーが認識されないコマンドを解析するコールバック。

詳細については、次を参照してください。 [DirectDraw ドライバーの初期化](directdraw-driver-initialization.md)します。

 

 





