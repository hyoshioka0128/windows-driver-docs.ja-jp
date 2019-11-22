---
title: Direct3D ドライバーの初期化
description: Direct3D ドライバーの初期化
ms.assetid: ef37a570-a94e-4021-b84f-4436aa454ac5
keywords:
- Direct3D ドライバーの初期化
- Direct3D WDK Windows 2000 display、initialization
- DrvGetDirectDrawInfo
- DdGetDriverInfo
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ebfaa21273c0d73df8ba8bbe50d264e639ae0948
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839011"
---
# <a name="direct3d-driver-initialization"></a>Direct3D ドライバーの初期化


## <span id="ddk_direct3d_driver_initialization_gg"></span><span id="DDK_DIRECT3D_DRIVER_INITIALIZATION_GG"></span>


ドライバーの[**DrvGetDirectDrawInfo**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgetdirectdrawinfo)関数が microsoft directdraw runtime によって呼び出されて directdraw サポートが初期化されると、ドライバーは次の処理を実行して microsoft Direct3D 機能を示す必要があります。

-   [**DD\_HALINFO**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_halinfo)構造体の Ddcaps **. dwcaps**メンバーで、ddcaps\_3d フラグを設定して、ドライバーのハードウェアに3d アクセラレーションがあることを示します。

-   HALINFO 構造体\_の DDSCAPS\_*Xxx*フラグを**設定します。このメンバーは**、ドライバーのビデオメモリサーフェイスの3d 機能を記述します。 次の表に、フラグを示します。

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
    <td align="left"><p>ドライバーの表面を3D レンダリングの宛先として使用できることを示します。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>DDSCAPS_TEXTURE</p></td>
    <td align="left"><p>ドライバーの表面を3D テクスチャマッピングに使用できることを示します。</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>DDSCAPS_ZBUFFER</p></td>
    <td align="left"><p>ドライバーのサーフェイスを Z バッファーとして使用できることを示します。</p></td>
    </tr>
    </tbody>
    </table>

     

<!-- -->

-   ドライバーの[**Ddgetdriverinfo**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverinfo)コールバックを指すように、 [**DD\_HALINFO**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_halinfo)構造体の**getdriverinfo**メンバーを設定します。 また、ドライバーは、DD\_HALINFO 構造体の**dwFlags**メンバーで DDHALINFO\_GETDRIVERINFOSET フラグを設定して、 **Ddgetdriverinfo**コールバックが実装されていることを示す必要があります。

-   [**D3DHAL\_コールバック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_callbacks)構造体のメンバーを割り当てて初期化し、DD\_HALINFO 構造体の**lpD3DHALCallbacks**メンバーにこの構造体を返します。

-   [**D3DHAL\_GLOBALDRIVERDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_globaldriverdata)構造体のメンバーを割り当てて初期化し、DD\_HALINFO 構造体の**lpD3DGlobalDriverData**メンバーにこの構造体を返します。

ドライバーが Microsoft DirectX 7.0 を使用できることを示すには、次の手順を実行します。

-   Microsoft Direct3D ドライバーの初期化中に報告される[**D3DDEVICEDESC\_V1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3ddevicedesc_v1)構造体の**dwdevcaps**メンバーに D3DDEVCAPS\_DRAWPRIMITIVES2EX フラグを含めます。

-   **CREATESURFACEEX**Miscellaneous2Callbacks 構造体[ **\_** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_miscellaneous2callbacks)の**getdriverstate**、、および**destroyddlocal**メンバーを設定して、 **Ddgetdriverinfo**コールバックの guid\_Miscellaneous2Callbacks guid に応答します。 これらは、Direct3D ドライバーの適切なコールバックをポイントするように設定され、MISC2CB32\_CREATESURFACEEX、DDHAL\_MISC2CB32\_GETDRIVERSTATE、および DDHAL\_MISC2CB32 を使用し\_て、 **dwFlags**メンバーの中にあります。\_DESTROYDDLOCAL bit をそれぞれ破棄します。

[**DrvGetDirectDrawInfo**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgetdirectdrawinfo)が返された後、GDI はドライバーの初期化を完了するために、ドライバーの[**Ddgetdriverinfo**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverinfo)コールバックをさまざまな guid に対して複数回呼び出します。 **Ddgetdriverinfo**コールバックは、Direct3D をサポートするために次の guid に応答する必要があります。

<span id="GUID_D3DCallbacks3"></span><span id="guid_d3dcallbacks3"></span><span id="GUID_D3DCALLBACKS3"></span>GUID\_D3DCallbacks3  
ドライバーは、 [**D3DHAL\_CALLBACKS3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_callbacks3)構造体のメンバーを割り当てて初期化し、 [**DD\_getdriverinfodata**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_getdriverinfodata)構造体の**lpvdata**メンバーでこの構造体を返します。

<span id="GUID_Miscellaneous2Callbacks"></span><span id="guid_miscellaneous2callbacks"></span><span id="GUID_MISCELLANEOUS2CALLBACKS"></span>GUID\_Miscellaneous2Callbacks  
ドライバーは、 [**dd\_MISCELLANEOUS2CALLBACKS**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_miscellaneous2callbacks)構造体のメンバーを割り当てて初期化し、DD\_GETDRIVERINFODATA 構造体の**lpvdata**メンバーでこの構造体を返す必要があります。

<span id="GUID_D3DExtendedCaps"></span><span id="guid_d3dextendedcaps"></span><span id="GUID_D3DEXTENDEDCAPS"></span>GUID\_D3DExtendedCaps  
ドライバーは、 [**D3DHAL\_D3DEXTENDEDCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_d3dextendedcaps)構造体の適切なメンバーを割り当てて初期化し、DD\_GETDRIVERINFODATA 構造体の**lpvdata**メンバーにこの構造体を返します。

<span id="GUID_ZPixelFormats"></span><span id="guid_zpixelformats"></span><span id="GUID_ZPIXELFORMATS"></span>GUID\_Zピクセル形式  
ドライバーは、ドライバーがサポートするすべての Z バッファー形式に対して、 [**Ddピクセル形式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddpixelformat)の構造体の適切なメンバーを割り当てて初期化し、DD\_GETDRIVERINFODATA の**lpvdata**メンバーでこれらの構造体を返します。データ. ドライバーが[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)の実装で D3DDP2OP\_CLEAR 操作コードをサポートしている場合は、この GUID に応答する必要があります。

<span id="GUID_D3DParseUnknownCommandCallback"></span><span id="guid_d3dparseunknowncommandcallback"></span><span id="GUID_D3DPARSEUNKNOWNCOMMANDCALLBACK"></span>GUID\_D3DParseUnknownCommandCallback  
ドライバーは、Direct3D ランタイムの**D3DParseUnknownCommand**コールバックへのポインターを格納する必要があります。 ポインターは、DD\_GETDRIVERINFODATA 構造体の**Lpvdata**メンバーのドライバーに渡されます。 ドライバーの[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)コールバックは、ドライバーで認識されないコマンドを解析するために**D3DParseUnknownCommand**コールバックを呼び出します。

詳細については、「 [DirectDraw ドライバーの初期化](directdraw-driver-initialization.md)」を参照してください。

 

 





