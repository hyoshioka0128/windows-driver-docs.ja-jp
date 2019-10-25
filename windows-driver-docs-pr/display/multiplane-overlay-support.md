---
title: マルチプレーン オーバーレイのサポート
description: Multiplane オーバーレイは、Windows Display Driver Model (WDDM) 1.3 以降のドライバーでサポートされています。 この機能は Windows 8.1 以降の新機能です。
ms.assetid: 8B2F5497-554D-4D4A-B44E-985A9F89143D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 376894a3d327542af472a13d242d1c0f23a6c1f7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840541"
---
# <a name="multiplane-overlay-support"></a>マルチプレーン オーバーレイのサポート


Multiplane オーバーレイは、Windows Display Driver Model (WDDM) 1.3 以降のドライバーでサポートされています。 この機能は Windows 8.1 以降の新機能です。

これらのセクションでは、この機能をドライバーに実装する方法について説明します。

## <a name="multiplane-overlay-functions-called-by-user-mode-display-drivers"></a>ユーザーモードの表示ドライバーによって呼び出される multiplane オーバーレイ関数

オペレーティングシステムによって実装されているすべてのユーザーモードの multiplane オーバーレイ関数。

| 関数 | 説明 |
|:--|:--|
|[pfnPresentMultiPlaneOverlayCb (D3D)](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_presentmultiplaneoverlaycb)|ソースの multiplane オーバーレイ割り当てから宛先割り当てにコンテンツをコピーします。 Windows Display Driver Model (WDDM) 1.3 以降のユーザーモード表示ドライバーによって呼び出すことができます。|
|[pfnPresentMultiPlaneOverlayCb (DXGI)](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/nc-dxgiddi-pfnddxgiddi_present_multiplane_overlaycb)|ソースの multiplane オーバーレイ割り当てから宛先割り当てにコンテンツをコピーします。 WDDM 1.3 以降のユーザーモード表示ドライバーで呼び出すことができます。|

## <a name="multiplane-overlay-functions-implemented-by-the-user-mode-driver"></a>ユーザーモードドライバーによって実装される multiplane オーバーレイ関数

このセクションには、マルチ平面オーバーレイをサポートするために、Windows Display Driver Model (WDDM) 1.3 以降のユーザーモード表示ドライバーで実装する必要がある関数が含まれています。

ドライバーは、ユーザーモードのディスプレイドライバーのアダプター固有の[CreateDevice (D3D10)](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)関数の呼び出しで、 [DXGI1_3_DDI_BASE_FUNCTIONS](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi1_3_ddi_base_functions)構造体のメンバーを介して、DXGI multiplane オーバーレイ関数へのポインターを提供します。 詳細については、「 [DXGI DDI のサポート](supporting-the-dxgi-ddi.md)」を参照してください。

ドライバーは、ドライバーの[CreateDevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createdevice)関数の呼び出しで、 [D3DDDI_DEVICEFUNCS](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddi_devicefuncs)構造体のメンバーを通じて、Microsoft Direct3D multiplane オーバーレイ関数へのポインターを提供します。

マルチ平面オーバーレイをサポートするために、ユーザーモードドライバーが実装する必要があるすべての関数。

| 関数 | 説明 |
|:--|:--|
|[pfnCheckMultiPlaneOverlaySupport (D3D)](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_checkmultiplaneoverlaysupport)| Multiplane オーバーレイのハードウェアサポートの詳細を確認するために、Direct3D ランタイムによって呼び出されます。|
|[pfnCheckMultiPlaneOverlaySupport (DXGI)](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi1_2_ddi_base_functions)| Multiplane オーバーレイのハードウェアサポートの詳細を確認するために、Microsoft DirectX Graphics Infrastructure (DXGI) ランタイムによって呼び出されます。|
|[pfnGetMultiPlaneOverlayCaps](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi1_2_ddi_base_functions)| ユーザーモードの表示ドライバーが基本的なオーバーレイプレーン機能を取得するように要求するために、DXGI ランタイムによって呼び出されます。 必要に応じて、WDDM 1.3 以降のユーザーモード表示ドライバーによって実装されます。|
|[pfnGetMultiplaneOverlayGroupCaps](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi1_3_ddi_base_functions)| ユーザーモードの表示ドライバーがオーバーレイプレーンの機能のグループを取得するように要求するために、DXGI ランタイムによって呼び出されます。 必要に応じて、WDDM 1.3 以降のユーザーモード表示ドライバーによって実装されます。|
|[Pfnon Multiplan Eオーバーレイ (D3D)](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_presentmultiplaneoverlay)| アプリケーションがレンダリングを完了したことをユーザーモードのディスプレイドライバーに通知するために Direct3D ランタイムによって呼び出され、コピーまたは反転するか、ドライバーがカラー塗りつぶし操作を実行することによってソースサーフェイスを表示するように要求します。 は、マルチ平面オーバーレイをサポートする WDDM 1.3 以降のドライバーで実装する必要があります。|
|[Pfnon Multiplan Eオーバーレイ (DXGI)](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi1_3_ddi_base_functions)| アプリケーションがレンダリングを完了したことをユーザーモードのディスプレイドライバーに通知するために、DXGI ランタイムによって呼び出され、コピーまたは反転するか、ドライバーがカラー塗りつぶし操作を実行することによって、ドライバーがソースサーフェイスを表示するように要求します。 は、マルチ平面オーバーレイをサポートする WDDM 1.3 以降のドライバーで実装する必要があります。|
 
## <a name="multiplane-overlay-user-mode-structures-and-enumerations"></a>マルチプレーンオーバーレイのユーザーモード構造と列挙体

Multiplane オーバーレイデバイスドライバーインターフェイス (DDIs) で使用されるすべてのユーザーモード構造体と列挙体。

| DDI | 説明 |
|:--|:--|
|[D3DDDI_MULTIPLANE_ALLOCATION_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-d3dddi_multiplane_overlay_allocation_info)|Multiplane オーバーレイの割り当てに関する情報を指定します。|
|[D3DDDI_MULTIPLANE_OVERLAY_ATTRIBUTES](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddi_multiplane_overlay_attributes)| オーバーレイ平面属性を指定するために、ユーザーモードの表示ドライバーによって使用されます。|
|[D3DDDI_MULTIPLANE_OVERLAY_BLEND](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-_d3dddi_multiplane_overlay_blend)| オーバーレイ平面に対して実行される blend 操作を識別します。|
|[D3DDDI_MULTIPLANE_OVERLAY_CAPS](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-d3dddi_multiplane_overlay_caps)| オーバーレイ平面機能を指定するために、ユーザーモード表示ドライバーによって使用されます。|
|[D3DDDI_MULTIPLANE_OVERLAY_FEATURE_CAPS](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-_d3dddi_multiplane_overlay_feature_caps)| オーバーレイ機能を識別します。|
|[D3DDDI_MULTIPLANE_OVERLAY_FLAGS](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-_d3dddi_multiplane_overlay_flags)| オーバーレイ平面に対して実行するフリップ操作を識別します。|
|[D3DDDI_MULTIPLANE_OVERLAY_GROUP_CAPS](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-d3dddi_multiplane_overlay_group_caps)| オーバーレイ平面機能のグループを指定するために、ユーザーモード表示ドライバーによって使用されます。|
|[D3DDDI_MULTIPLANE_OVERLAY_GROUP_CAPS_INPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-d3dddi_multiplane_overlay_group_caps_input)| Multiplane オーバーレイ機能グループに関する情報を指定します。|
|[D3DDDI_MULTIPLANE_OVERLAY_STRETCH_QUALITY](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-d3dddi_multiplane_overlay_stretch_quality)| マルチプレーンオーバーレイデータを拡大または縮小するときにハードウェアが実行する必要があるフィルター処理を識別します。
|[D3DDDI_MULTIPLANE_OVERLAY_VIDEO_FRAME_FORMAT](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-d3dddi_multiplane_overlay_video_frame_format)|オーバーレイ平面のビデオフレーム形式を識別します。 D3DDDI_MULTIPLANE_OVERLAY_VIDEO_FRAME_FORMAT_PROGRESSIVE 値のみがサポートされています。|
|[D3DDDI_MULTIPLANE_OVERLAY_YCbCr_FLAGS](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-d3dddi_multiplane_overlay_ycbcr_flags)| Multiplane オーバーレイを説明する YUV 範囲と変換情報を識別します。|
|[D3DDDI_PRESENT_MULTIPLANE_OVERLAY](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddi_present_multiplane_overlay)| 表示するオーバーレイ平面を指定します。|
|[D3DDDIARG_CHECKMULTIPLANEOVERLAYSUPPORT](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_checkmultiplaneoverlaysupport)| PfnCheckMultiPlaneOverlaySupport (D3D) 関数の呼び出しで、multiplane オーバーレイのハードウェアサポートの詳細を確認するために使用されます。|
|[D3DDDIARG_PRESENTMULTIPLANEOVERLAY](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-d3dddiarg_presentmultiplaneoverlay)| 表示する multiplane オーバーレイリソースを指定します。|
|[D3DDDICB_PRESENTMULTIPLANEOVERLAY](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-d3dddicb_presentmultiplaneoverlay)| コンテンツのコピー元またはコピー元となる multiplane のオーバーレイの割り当てについて説明します。|
 
## <a name="multiplane-overlay-kernel-mode-driver-implemented-functions"></a>Multiplane オーバーレイカーネルモードドライバーで実装された関数

ディスプレイミニポートドライバーによって実装されるすべての multiplane オーバーレイ関数。

|関数|説明|
|:--|:--|
|[DXGKDDI_CHECKMULTIPLANEOVERLAYSUPPORT](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_checkmultiplaneoverlaysupport)| Multiplane オーバーレイのハードウェアサポートの詳細を確認するために、Microsoft DirectX graphics カーネルサブシステムによって呼び出されます。|
|[DXGKDDI_CHECKMULTIPLANEOVERLAYSUPPORT3](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_checkmultiplaneoverlaysupport3)| 次の新しい関数は、特定のマルチプレーンオーバーレイ構成がサポートされているかどうかを判断するために呼び出されます。|
|[DXGKDDI_GETMULTIPLANEOVERLAYCAPS](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_getmultiplaneoverlaycaps)| Multiplane オーバーレイ機能を取得するために呼び出されます。 複数のプレーンをサポートする WDDM 2.2 ドライバーでは、この DDI のサポートが必要です。|
|[DXGKDDI_POSTMULTIPLANEOVERLAYPRESENT](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_postmultiplaneoverlaypresent)| 新しいマルチプレーンオーバーレイ構成が有効になった後に呼び出され、ドライバーがハードウェアの状態を最適化できるようにします。 マルチプレーンオーバーレイをサポートする Windows Display Driver Model (WDDM) 2.0 以降のドライバーでは省略可能です。|
|[DXGKDDI_SETVIDPNSOURCEADDRESSWITHMULTIPLANEOVERLAY3](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_setvidpnsourceaddresswithmultiplaneoverlay3)|表示されるオーバーレイ構成を変更するために呼び出されます。|
|[DXGKDDI_CHECKMULTIPLANEOVERLAYSUPPORT2](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_checkmultiplaneoverlaysupport2)|DxgkDdiCheckMultiPlaneOverlaySupport2 は、特定のマルチプレーンオーバーレイ構成がサポートされているかどうかを判断するために呼び出されます。 |
|[DXGKDDI_SETVIDPNSOURCEADDRESSWITHMULTIPLANEOVERLAY](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_setvidpnsourceaddresswithmultiplaneoverlay)|特定のビデオが存在するソースに関連付けられている、デスクトップウィンドウマネージャー (DWM) のスワップチェーンを含む複数のサーフェスのアドレスを設定します。 この関数は、複数のサーフェイス (DWM のスワップチェーンを含む) を画面に表示するために使用されます。|
|[DXGKDDI_SETVIDPNSOURCEADDRESSWITHMULTIPLANEOVERLAY2](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_setvidpnsourceaddresswithmultiplaneoverlay2)| DxgkDdiSetVidPnSourceAddressWithMultiPlaneOverlay2 は、表示されるオーバーレイ構成を変更するために呼び出されます。|

## <a name="multiplane-overlay-kernel-mode-structures"></a>Multiplane オーバーレイカーネルモード構造体

によって使用されるすべての構造体は、ミニポートドライバーを表示します。

|構造体|説明|
|:--|:--|
|[DXGK_CHECK_MULTIPLANE_OVERLAY_SUPPORT_PLANE](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_check_multiplane_overlay_support_plane)| マルチ平面オーバーレイに対してハードウェアが提供するサポート属性を指定します。|
|[DXGK_CHECK_MULTIPLANE_OVERLAY_SUPPORT_RETURN_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-dxgk_check_multiplane_overlay_support_return_info)| マルチプレーンオーバーレイのハードウェアサポートに関する制限を指定します。|
|[DXGK_MULTIPLANE_OVERLAY_ATTRIBUTES](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_multiplane_overlay_attributes)| オーバーレイ平面属性を指定するために、ディスプレイミニポートドライバーによって使用されます。|
|[DXGK_MULTIPLANE_OVERLAY_ATTRIBUTES2](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_multiplane_overlay_attributes2)|DXGK_MULTIPLANE_OVERLAY_ATTRIBUTES2 は、オーバーレイ平面属性を指定するためにディスプレイミニポートドライバーによって使用されます。 |
|[DXGK_MULTIPLANE_OVERLAY_BLEND](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_multiplane_overlay_blend)| オーバーレイ平面に対して実行される blend 操作を識別します。|
|[DXGK_MULTIPLANE_OVERLAY_FLAGS](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_multiplane_overlay_flags)| オーバーレイ平面に対して実行するフリップ操作を識別します。|
|[DXGK_MULTIPLANE_OVERLAY_PLANE](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_multiplane_overlay_plane)| DxgkDdiSetVidPnSourceAddressWithMultiPlaneOverlay 関数の呼び出しに表示するオーバーレイ平面を指定します。|
|[DXGK_MULTIPLANE_OVERLAY_PLANE2](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_multiplane_overlay_plane2)|DXGK_MULTIPLANE_OVERLAY_PLANE2 は、表示するオーバーレイ平面を指定するために DxgkDdiSetVidPnSourceAddressWithMultiPlaneOverlay2 関数と共に使用されます。|
|[DXGK_MULTIPLANE_OVERLAY_PLANE_WITH_SOURCE](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_multiplane_overlay_plane_with_source)|DXGK_MULTIPLANE_OVERLAY_PLANE_WITH_SOURCE では、マルチプレーンオーバーレイプレーンの属性、割り当て、およびビデオに含まれるネットワークソースの識別番号について説明します。|
|[DXGK_MULTIPLANE_OVERLAY_VSYNC_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_multiplane_overlay_vsync_info)|垂直同期間隔中に表示するオーバーレイ平面を指定します。|
|[DXGK_MULTIPLANE_OVERLAY_YCbCr_FLAGS](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_multiplane_overlay_ycbcr_flags)|Multiplane オーバーレイを説明する YUV 範囲と変換情報を識別します。|
|[DXGK_PRESENTMULTIPLANEOVERLAYINFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_presentmultiplaneoverlayinfo)|VidPN 入力と表示するオーバーレイ平面に関する情報を指定します。|
|[DXGK_PRESENTMULTIPLANEOVERLAYLIST](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_presentmultiplaneoverlaylist)|DxgkDdiPresent 関数の呼び出しに表示するオーバーレイ平面を指定します。|
|[DXGKARG_CHECKMULTIPLANEOVERLAYSUPPORT](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_checkmultiplaneoverlaysupport)|DxgkDdiCheckMultiPlaneOverlaySupport 関数の呼び出しで、multiplane オーバーレイのハードウェアサポートの詳細を確認するために使用されます。|
|[DXGKARG_CHECKMULTIPLANEOVERLAYSUPPORT2](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_checkmultiplaneoverlaysupport2)|DXGKARG_CHECKMULTIPLANEOVERLAYSUPPORT2 は、特定のマルチプレーンオーバーレイ構成がサポートされているかどうかを判断するために DxgkDdiCheckMultiPlaneOverlaySupport2 関数に渡されます。|
|[DXGKARG_SETVIDPNSOURCEADDRESSWITHMULTIPLANEOVERLAY](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_setvidpnsourceaddresswithmultiplaneoverlay)|DxgkDdiSetVidPnSourceAddressWithMultiPlaneOverlay 関数の引数を格納します。|
|[DXGKARG_SETVIDPNSOURCEADDRESSWITHMULTIPLANEOVERLAY2](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_setvidpnsourceaddresswithmultiplaneoverlay2)|DXGKARG_SETVIDPNSOURCEADDRESSWITHMULTIPLANEOVERLAY2 は、表示されるオーバーレイ構成を変更するために DxgkDdiSetVidPnSourceAddressWithMultiPlaneOverlay2 関数に渡されます。|
 

## <a name="multiplane-overlay-kernel-mode-enumerations"></a>Multiplane オーバーレイカーネルモード列挙型

ミニポートドライバーの表示によって使用されるすべての列挙体。

| 列挙値 | 説明 |
|:--|:--|
|[DXGK_MULTIPLANE_OVERLAY_STEREO_FLIP_MODE](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ne-d3dkmddi-_dxgk_multiplane_overlay_stereo_flip_mode)|オーバーレイ平面のステレオフリップモードを識別します。 DXGK_MULTIPLANE_OVERLAY_STEREO_FLIP_NONE 値のみがサポートされています。 |
|[DXGK_MULTIPLANE_OVERLAY_STEREO_FORMAT](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ne-d3dkmddi-_dxgk_multiplane_overlay_stereo_format)|オーバーレイ平面のステレオプレゼンテーション形式を識別します。 DXGK_MULTIPLANE_OVERLAY_STEREO_FORMAT_MONO 値のみがサポートされています。|
|[DXGK_MULTIPLANE_OVERLAY_STRETCH_QUALITY](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ne-d3dkmddi-_dxgk_multiplane_overlay_stretch_quality)|マルチプレーンオーバーレイデータを拡大または縮小するときにハードウェアが実行する必要があるフィルター処理を識別します。|
|[DXGK_MULTIPLANE_OVERLAY_VIDEO_FRAME_FORMAT](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ne-d3dkmddi-_dxgk_multiplane_overlay_video_frame_format)|オーバーレイ平面のビデオフレーム形式を識別します。 DXGK_MULTIPLANE_OVERLAY_VIDEO_FRAME_FORMAT_PROGRESSIVE 値のみがサポートされています。|
 

このユーザーモード列挙定数値は、multiplane オーバーレイをサポートし、Windows 8.1 に新しく追加されています。

-   [**D3DDDICAPS\_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-_d3dddicaps_type) ( **\_D3DDDICAPS\_MULTIPLANE\_オーバーレイ\_グループ\_CAPS**定数値)

 

 





