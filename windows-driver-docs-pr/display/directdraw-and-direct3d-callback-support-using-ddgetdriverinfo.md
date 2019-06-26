---
title: DirectDraw と DdGetDriverInfo を使用して、D3D のコールバック サポート
description: ディスプレイ ドライバーは、さまざまな DirectDraw、Direct3D のコールバック サポートを示すため DdGetDriverInfo 関数を実装できます。
ms.assetid: 7054564e-4520-4900-946a-95c92908667c
keywords:
- Windows 2000、Windows 2000 の WDK 表示 DirectDraw ドライバーの初期化
- WDK DirectDraw のコールバック関数
- DdGetDriverInfo
- Direct3D WDK Windows 2000 の表示、コールバック
- WDK Direct3D のコールバック関数
- DirectDraw ドライバー WDK Windows 2000 の表示、コールバック関数の初期化
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: a2747373a5496aa32f380000cd5af991f479d611
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384857"
---
# <a name="directdraw-and-direct3d-callback-support-using-ddgetdriverinfo"></a>DdGetDriverInfo を使用した DirectDraw および Direct3D コールバックのサポート

ディスプレイ ドライバーが実装できる、 [ **DdGetDriverInfo** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverinfo) DirectDraw、Direct3D のさまざまなコールバックのサポートを示すための関数。 コールバックのサポートは、ドライバーが受信した次の Guid に基づく、 **guidInfo**のメンバー、 [ **DD\_GETDRIVERINFODATA** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_getdriverinfodata)構造体*lpGetDriverInfo*パラメーター ポイント。 ドライバーで構造体へのポインターを返します、 **lpvData** DirectDraw を指定するメンバーまたは Direct3D コールバックのサポート。

- ドライバーは、GUID を受け取る場合\_ColorControlCallbacks の GUID へのポインターを返します、 [ **DD\_COLORCONTROLCALLBACKS** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_colorcontrolcallbacks)構造体。 サポートしている場合[コントロールの色](color-control-initialization.md)、ドライバーの塗りつぶし、 **ColorControl** DD のメンバー\_COLORCONTROLCALLBACKS を指定するその[ *DdControlColor*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_colorcb_colorcontrol)コールバック関数。

- ドライバーは、GUID を受け取る場合\_D3DCallbacks、GUID\_D3DCallbacks3、または GUID\_Miscellaneous2Callbacks の GUID へのポインターを返します、 [ **D3DHAL\_コールバック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_callbacks)、 [ **D3DHAL\_CALLBACKS3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_callbacks3)、または[ **DD\_MISCELLANEOUS2CALLBACKS** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_miscellaneous2callbacks)構造体。 ドライバーを示すためにこれらの構造を使用してその[Direct3D のコールバック サポート](driver-functions-to-support-direct3d.md)します。 詳細については、次を参照してください。 [Direct3D DDI](direct3d.md)します。

- ドライバーは、GUID を受け取る場合\_KernelCallbacks の GUID へのポインターを返します、 [ **DD\_KERNELCALLBACKS** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_kernelcallbacks)構造体。 ドライバーが DD のメンバー\_KERNELCALLBACKS を次のコールバック関数をサポートしていることを示します。

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
  <td align="left"><p>設定し、画面のデータを変更します。</p></td>
  </tr>
  <tr class="even">
  <td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_kernelcb_syncvideoport" data-raw-source="[&lt;em&gt;DdSyncVideoPortData&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_kernelcb_syncvideoport)"><em>DdSyncVideoPortData</em></a></p></td>
  <td align="left"><p>設定し、ビデオ ポート (VPE) の拡張機能のオブジェクトのデータを変更します。</p></td>
  </tr>
  </tbody>
  </table>

- ドライバーは、GUID を受け取る場合\_MiscellaneousCallbacks の GUID へのポインターを返します、 [ **DD\_MISCELLANEOUSCALLBACKS** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_miscellaneouscallbacks)構造体。 サポートしている場合、 [ *DdGetAvailDriverMemory* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getavaildrivermemory)コールバック関数では、ドライバーの塗りつぶし、 *DdGetAvailDriverMemory* DD のメンバー\_指定する MISCELLANEOUSCALLBACKS *DdGetAvailDriverMemory*します。

- ドライバーは、GUID を受け取る場合\_MotionCompCallbacks の GUID へのポインターを返します、 [ **DD\_MOTIONCOMPCALLBACKS** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks) のサポートを示す構造[補正コールバックのモーション](motion-compensation-callbacks.md)します。 詳細については、次を参照してください。[圧縮されたビデオのデコード](compressed-video-decoding.md)します。

- ドライバーは、GUID を受け取る場合\_NTCallbacks の GUID へのポインターを返します、 [ **DD\_NTCALLBACKS** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_ntcallbacks)構造体。 ドライバーが DD のメンバー\_NTCALLBACKS を次のコールバック関数をサポートしていることを示します。

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
  <td align="left"><p>GDI サーフェイスとの間、DirectDraw を反転ドライバーに通知します。</p></td>
  </tr>
  <tr class="even">
  <td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_freedrivermemory" data-raw-source="[&lt;em&gt;DdFreeDriverMemory&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_freedrivermemory)"><em>DdFreeDriverMemory</em></a></p></td>
  <td align="left"><p>新しい割り当て要求を満たすためにオフスクリーンまたは非表示のメモリを解放します。</p></td>
  </tr>
  <tr class="odd">
  <td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_setexclusivemode" data-raw-source="[&lt;em&gt;DdSetExclusiveMode&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_setexclusivemode)"><em>DdSetExclusiveMode</em></a></p></td>
  <td align="left"><p>排他モードとの間、DirectDraw アプリケーションを切り替えるときに、ドライバーに通知します。</p></td>
  </tr>
  </tbody>
  </table>

     

<!-- -->

-   ドライバーは、GUID を受け取る場合\_VideoPortCallbacks の GUID へのポインターを返します、 [ **DD\_VIDEOPORTCALLBACKS** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_videoportcallbacks) のサポートを示す構造[VPE コールバック関数](vpe-callback-functions.md)します。 詳細については、次を参照してください。 [DirectX の拡張機能のビデオ ポート](video-port-extensions-to-directx.md)します。

 

 





