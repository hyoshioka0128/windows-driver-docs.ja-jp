---
title: Multiplane オーバーレイ VidPN プレゼンテーション
ms.assetid: BAD7FD48-905D-4547-8C69-133240B39FA3
description: 複数のサーフェイスに存在するために使用される関数に適用される要件。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06b5c799a1de5084374d27c9ce273a995133ad59
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840538"
---
# <a name="multiplane-overlay-vidpn-presentation"></a>Multiplane オーバーレイ VidPN プレゼンテーション


Multiplane オーバーレイが使用されている場合、これらの要件は、ビデオの現在のネットワーク (VidPNs) の複数のサーフェイスに存在する関数に適用されます。

<span id="DxgkDdiSetVidPnSourceAddressWithMultiPlaneOverlay"></span><span id="dxgkddisetvidpnsourceaddresswithmultiplaneoverlay"></span><span id="DXGKDDISETVIDPNSOURCEADDRESSWITHMULTIPLANEOVERLAY"></span>[*DxgkDdiSetVidPnSourceAddressWithMultiPlaneOverlay*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_setvidpnsourceaddresswithmultiplaneoverlay)  
-   [**DXGK\_multiplane\_\_平面にオーバーレイ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_multiplane_overlay_plane)します。**有効**になっている場合は、ミニポートドライバーによって、指定された平面が無効になります。
-   以前に[*DxgkDdiSetVidPnSourceAddressWithMultiPlaneOverlay*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_setvidpnsourceaddresswithmultiplaneoverlay)を呼び出したときに平面が有効になっていたが、現在の呼び出しには存在しない場合、ドライバーは、反転せずに平面を表示し続ける必要があります。
-   同じ垂直同期 (1 つの平面を反転するための1つの呼び出しと、別の平面を反転するための呼び出し) 中に、ドライバーが[*DxgkDdiSetVidPnSourceAddressWithMultiPlaneOverlay*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_setvidpnsourceaddresswithmultiplaneoverlay)の複数の呼び出しを受信する可能性があります。 この場合、ドライバーは両方の呼び出しを処理する必要があります。
-   渡されたデータは、信頼できるソースによってユーザーモードで検証されている必要があります。 ただし、ディスプレイミニポートドライバーでは、問題が発生しないことを確認するためにデータを確認する必要があります。 データが正しくない場合、ドライバーは、**状態\_無効\_パラメーター**エラーコードを含む呼び出しを失敗させる可能性がありますが、このようなエラーは適切に処理されず、オペレーティングシステムまたはユーザーモードドライバーのバグを意味します。

<span id="DxgkDdiSetVidPnSourceVisibility"></span><span id="dxgkddisetvidpnsourcevisibility"></span><span id="DXGKDDISETVIDPNSOURCEVISIBILITY"></span>[*DxgkDdiSetVidPnSourceVisibility*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_setvidpnsourcevisibility)  
[**Dxgkarg\_SETVIDPNSOURCEVISIBILITY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_setvidpnsourcevisibility)。この関数の呼び出しでは、指定されたソースで**Visible**が**FALSE**に設定されています。プライマリサーフェイスに使用されるレイヤーを含め、すべてのハードウェアプレーンが無効になっている必要があります。 **Visible**が**TRUE**に設定されている場合、プライマリサーフェイスに使用されている平面のみが有効になっている必要があり、その他のすべてのプレーンは無効のままにしておく必要があります。

<span id="DxgkDdiSetVidPnSourceAddress"></span><span id="dxgkddisetvidpnsourceaddress"></span><span id="DXGKDDISETVIDPNSOURCEADDRESS"></span>[*DxgkDdiSetVidPnSourceAddress*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff560767(v=vs.85))  
この関数が呼び出されると、ドライバーは非プライマリオーバーレイプレーンをすべて無効にする必要があります。 マルチ平面オーバーレイモードでは、 [*DxgkDdiSetVidPnSourceAddressWithMultiPlaneOverlay*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_setvidpnsourceaddresswithmultiplaneoverlay)を使用してプライマリサーフェイスが反転されます。

 

 





