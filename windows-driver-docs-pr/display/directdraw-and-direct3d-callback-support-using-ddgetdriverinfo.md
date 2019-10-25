---
title: DdGetDriverInfo を使用した DirectDraw および D3D コールバックのサポート
description: ディスプレイドライバーは、さまざまな DirectDraw および Direct3D コールバックサポートを示すために、DdGetDriverInfo 関数を実装できます。
ms.assetid: 7054564e-4520-4900-946a-95c92908667c
keywords:
- DirectDraw ドライバー初期化 WDK Windows 2000 display、Windows 2000
- コールバック関数 WDK DirectDraw
- DdGetDriverInfo
- Direct3D WDK Windows 2000 display、コールバック
- コールバック関数 WDK Direct3D
- DirectDraw ドライバー初期化 WDK Windows 2000 display, callback 関数
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 7f546f5e74def26fb93afeffd88d213120eda6ac
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838999"
---
# <a name="directdraw-and-direct3d-callback-support-using-ddgetdriverinfo"></a>DdGetDriverInfo を使用した DirectDraw および Direct3D コールバックのサポート

ディスプレイドライバーは、さまざまな DirectDraw および Direct3D コールバックサポートを示すために、 [**Ddgetdriverinfo**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverinfo)関数を実装できます。 コールバックのサポートは、 *lpgetdriverinfo*パラメーターによって指定される、 [**DD\_GETDRIVERINFODATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_getdriverinfodata)構造体の**guidinfo**メンバーでドライバーが受信する次の guid に対して決まります。 ドライバーは、DirectDraw または Direct3D コールバックのサポートを指定する、 **Lpvdata**メンバー内の構造体へのポインターを返します。

- ドライバーが ColorControlCallbacks バック GUID\_GUID を受け取ると、 [**DD\_COLORCONTROLCALLBACKS バック**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_colorcontrolcallbacks)構造体へのポインターが返されます。 [カラーコントロール](color-control-initialization.md)がサポートされている場合、ドライバーは、DD\_colorcontrolcallback の**colorcontrol**メンバーに入力して、 [*ddcontrolcolor*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_colorcb_colorcontrol)コールバック関数を指定します。

- ドライバーが GUID\_D3DCallbacks、GUID\_D3DCallbacks3、または GUID\_Miscellaneous2Callbacks GUID を受け取ると、 [**D3DHAL\_コールバック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_callbacks)、 [**D3DHAL\_CALLBACKS3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_callbacks3)、または DD へのポインターが返され[ **\_MISCELLANEOUS2CALLBACKS**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_miscellaneous2callbacks)構造体。 ドライバーは、これらの構造体を使用して、 [Direct3D コールバックサポート](driver-functions-to-support-direct3d.md)を示します。 詳細については、「 [DIRECT3D DDI](direct3d.md)」を参照してください。

- ドライバーが\_のカーネルコールバック GUID を受け取ると、 [**DD\_のカーネルコールバック**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_kernelcallbacks)構造へのポインターが返されます。 このドライバーは、次のコールバック関数をサポートしていることを示すために、DD のメンバーを\_します。

  <table>
  <colgroup>
  <col width="50%" />
  <col width="50%" />
  </colgroup>
  <thead>
  <tr class="header">
  <th align="left">コールバック関数</th>
  <th align="left">説明</th>
  </tr>
  </thead>
  <tbody>
  <tr class="odd">
  <td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_kernelcb_syncsurface" data-raw-source="[&lt;em&gt;DdSyncSurfaceData&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_kernelcb_syncsurface)"><em>DdSyncSurfaceData</em></a></p></td>
  <td align="left"><p>サーフェイスデータを設定および変更します。</p></td>
  </tr>
  <tr class="even">
  <td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_kernelcb_syncvideoport" data-raw-source="[&lt;em&gt;DdSyncVideoPortData&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_kernelcb_syncvideoport)"><em>DdSyncVideoPortData</em></a></p></td>
  <td align="left"><p>ビデオポート拡張 (VPE) オブジェクトデータを設定および変更します。</p></td>
  </tr>
  </tbody>
  </table>

- ドライバーが GUID\_MiscellaneousCallbacks GUID を受け取ると、 [**DD\_MiscellaneousCallbacks**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_miscellaneouscallbacks)構造体へのポインターが返されます。 [*Ddgetavailability drivermemory*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getavaildrivermemory)コールバック関数がサポートされている場合、ドライバーは、DD\_MISCELLANEOUSCALLBACKS の*ddgetavailability drivermemory*メンバーをいっぱいにして、 *ddgetavailability drivermemory*を指定します。

- ドライバーは、MotionCompCallbacks バック GUID\_GUID を受け取ると、 [**DD\_MOTIONCOMPCALLBACKS**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)バック構造へのポインターを返して、[モーション補正コールバック](motion-compensation-callbacks.md)のサポートを示します。 詳細については、「[圧縮ビデオのデコード](compressed-video-decoding.md)」を参照してください。

- ドライバーが NTCallbacks バック GUID\_GUID を受け取ると、 [**DD\_NTCALLBACKS バック**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_ntcallbacks)構造へのポインターが返されます。 このドライバーは、次のコールバック関数をサポートしていることを示すために、DD\_NTCALLBACKS のメンバーを埋め込みます。

  <table>
  <colgroup>
  <col width="50%" />
  <col width="50%" />
  </colgroup>
  <thead>
  <tr class="header">
  <th align="left">コールバック関数</th>
  <th align="left">説明</th>
  </tr>
  </thead>
  <tbody>
  <tr class="odd">
  <td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_fliptogdisurface" data-raw-source="[&lt;em&gt;DdFlipToGDISurface&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_fliptogdisurface)"><em>DdFlipToGDISurface</em></a></p></td>
  <td align="left"><p>DirectDraw が GDI サーフェイスとの間で反転するときに、ドライバーに通知します。</p></td>
  </tr>
  <tr class="even">
  <td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_freedrivermemory" data-raw-source="[&lt;em&gt;DdFreeDriverMemory&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_freedrivermemory)"><em>DdFreeDriverMemory</em></a></p></td>
  <td align="left"><p>新しい割り当て要求を満たすために、スクリーンオフまたは非ローカルの表示メモリを解放します。</p></td>
  </tr>
  <tr class="odd">
  <td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_setexclusivemode" data-raw-source="[&lt;em&gt;DdSetExclusiveMode&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_setexclusivemode)"><em>DdSetExclusiveMode</em></a></p></td>
  <td align="left"><p>DirectDraw アプリケーションが排他モードに切り替えているときに、ドライバーに通知します。</p></td>
  </tr>
  </tbody>
  </table>

     

<!-- -->

-   ドライバーが\_Videoportcallbacks GUID を受け取ると、オブジェクトは、 [ **\_Videoportcallbacks**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_videoportcallbacks)構造体へのポインターを返して、 [VPE コールバック関数](vpe-callback-functions.md)のサポートを示します。 詳細については、「 [DirectX のビデオポート拡張](video-port-extensions-to-directx.md)」を参照してください。

 

 





