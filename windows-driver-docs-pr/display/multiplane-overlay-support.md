---
title: マルチプレーン オーバーレイのサポート
description: Multiplane オーバーレイは、Windows Display Driver Model (WDDM) 1.3 およびそれ以降のドライバーによってサポートできます。 この機能は、新しい Windows 8.1 以降です。
ms.assetid: 8B2F5497-554D-4D4A-B44E-985A9F89143D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be2a343b1e869aae780dc705d7ca7dc63a8e6bf1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372833"
---
# <a name="multiplane-overlay-support"></a>マルチプレーン オーバーレイのサポート


Multiplane オーバーレイは、Windows Display Driver Model (WDDM) 1.3 およびそれ以降のドライバーによってサポートできます。 この機能は、新しい Windows 8.1 以降です。

これらのセクションには、ドライバーでこの機能を実装する方法について説明します。

## <a name="multiplane-overlay-functions-called-by-user-mode-display-drivers"></a>Multiplane オーバーレイ関数が呼び出したユーザー モード ドライバーを表示します。

オペレーティング システムを実装するすべてのユーザー モード multiplane オーバーレイ関数。

| 関数 | 説明 |
|:--|:--|
|[pfnPresentMultiPlaneOverlayCb (D3D)](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_presentmultiplaneoverlaycb)|ソース multiplane から内容をコピー先の割り当てへの割り当てをオーバーレイします。 Windows 表示 Driver Model (WDDM) 1.3 またはそれ以降のユーザー モードのディスプレイ ドライバーから呼び出すことができます。|
|[pfnPresentMultiPlaneOverlayCb (DXGI)](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/nc-dxgiddi-pfnddxgiddi_present_multiplane_overlaycb)|ソース multiplane から内容をコピー先の割り当てへの割り当てをオーバーレイします。 WDDM 1.3 またはそれ以降のユーザー モードのディスプレイ ドライバーから呼び出すことができます。|

## <a name="multiplane-overlay-functions-implemented-by-the-user-mode-driver"></a>ユーザー モード ドライバーによって実装される multiplane オーバーレイ関数

このセクションには、Windows 表示 Driver Model (WDDM) 1.3 およびそれ以降のユーザー モードのディスプレイ ドライバーが multiplane オーバーレイをサポートするために実装する必要があります関数が含まれています。

ドライバーのメンバーを使用して DXGI multiplane オーバーレイ関数へのポインターを提供する、 [DXGI1_3_DDI_BASE_FUNCTIONS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi1_3_ddi_base_functions)ユーザー モードのディスプレイ ドライバーへの呼び出しで構造体のアダプター固有[CreateDevice(D3D10)](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)関数。 詳細については、次を参照してください。 [DXGI DDI をサポートしている](supporting-the-dxgi-ddi.md)します。

ドライバーのメンバーを使用してマイクロソフトの Direct3D multiplane オーバーレイ関数へのポインターを提供する、 [D3DDDI_DEVICEFUNCS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddi_devicefuncs)ドライバーの呼び出しで構造[CreateDevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createdevice)関数。

Multiplane オーバーレイをサポートするために、ユーザー モード ドライバーを実装する必要がありますすべての機能です。

| 関数 | 説明 |
|:--|:--|
|[pfnCheckMultiPlaneOverlaySupport (D3D)](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_checkmultiplaneoverlaysupport)| Multiplane オーバーレイのハードウェア サポートの詳細を確認する Direct3D のランタイムによって呼び出されます。|
|[pfnCheckMultiPlaneOverlaySupport (DXGI)](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi1_2_ddi_base_functions)| Multiplane オーバーレイのハードウェア サポートの詳細を確認する Microsoft DirectX Graphics Infrastructure (DXGI) ランタイムによって呼び出されます。|
|[pfnGetMultiPlaneOverlayCaps](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi1_2_ddi_base_functions)| ユーザー モードのディスプレイ ドライバーが基本的なオーバーレイ平面の機能を取得することを要求する DXGI ランタイムによって呼び出されます。 必要に応じて、WDDM 1.3 およびそれ以降のユーザー モードのディスプレイ ドライバーによって実装されます。|
|[pfnGetMultiplaneOverlayGroupCaps](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi1_3_ddi_base_functions)| ユーザー モードがオーバーレイ平面の機能のグループについてドライバー get を表示していることを要求する DXGI ランタイムによって呼び出されます。 必要に応じて、WDDM 1.3 およびそれ以降のユーザー モードのディスプレイ ドライバーによって実装されます。|
|[pfnPresentMultiplaneOverlay (D3D)](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_presentmultiplaneoverlay)| アプリケーションには、レンダリングと、ドライバーがコピーまたは反転のいずれかによってソース画面を表示する要求が完了したこと、またはドライバーが塗りつぶしの色の操作を実行するユーザー モードのディスプレイ ドライバーに通知する Direct3D のランタイムによって呼び出されます。 WDDM 1.3 または multiplane オーバーレイをサポートするドライバーを後で実装しなければなりません。|
|[pfnPresentMultiplaneOverlay (DXGI)](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi1_3_ddi_base_functions)| アプリケーションには、レンダリングと、ドライバーがコピーまたは反転のいずれかによってソース画面を表示する要求が完了したこと、またはドライバーが塗りつぶしの色の操作を実行するユーザー モードのディスプレイ ドライバーに通知する DXGI ランタイムによって呼び出されます。 WDDM 1.3 または multiplane オーバーレイをサポートするドライバーを後で実装しなければなりません。|
 
## <a name="multiplane-overlay-user-mode-structures-and-enumerations"></a>Multiplane オーバーレイ ユーザー モードの構造および列挙体

すべてのユーザー モードの構造および multiplane で使用される列挙体は、デバイス ドライバー インターフェイス (Ddi) をオーバーレイします。

| DDI | 説明 |
|:--|:--|
|[D3DDDI_MULTIPLANE_ALLOCATION_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-d3dddi_multiplane_overlay_allocation_info)|Multiplane オーバーレイ割り当てに関する情報を指定します。|
|[D3DDDI_MULTIPLANE_OVERLAY_ATTRIBUTES](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddi_multiplane_overlay_attributes)| ユーザー モードのディスプレイ ドライバーによってオーバーレイ平面の属性を指定するために使用します。|
|[D3DDDI_MULTIPLANE_OVERLAY_BLEND](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ne-d3dumddi-_d3dddi_multiplane_overlay_blend)| オーバーレイ平面に実行する合成操作を識別します。|
|[D3DDDI_MULTIPLANE_OVERLAY_CAPS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-d3dddi_multiplane_overlay_caps)| ユーザー モードのディスプレイ ドライバーによってオーバーレイ平面の機能を指定するために使用します。|
|[D3DDDI_MULTIPLANE_OVERLAY_FEATURE_CAPS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ne-d3dumddi-_d3dddi_multiplane_overlay_feature_caps)| オーバーレイの機能を識別します。|
|[D3DDDI_MULTIPLANE_OVERLAY_FLAGS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ne-d3dumddi-_d3dddi_multiplane_overlay_flags)| オーバーレイ平面に実行する反転操作を識別します。|
|[D3DDDI_MULTIPLANE_OVERLAY_GROUP_CAPS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-d3dddi_multiplane_overlay_group_caps)| ユーザー モードのディスプレイ ドライバーによって使用すると、オーバーレイ平面の機能のグループを指定します。|
|[D3DDDI_MULTIPLANE_OVERLAY_GROUP_CAPS_INPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-d3dddi_multiplane_overlay_group_caps_input)| Multiplane オーバーレイの機能グループの情報を指定します。|
|[D3DDDI_MULTIPLANE_OVERLAY_STRETCH_QUALITY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ne-d3dumddi-d3dddi_multiplane_overlay_stretch_quality)| ハードウェアが拡大または multiplane オーバーレイ データを圧縮するときに実行する必要がありますフィルタ リングのプロセスを識別します。
|[D3DDDI_MULTIPLANE_OVERLAY_VIDEO_FRAME_FORMAT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ne-d3dumddi-d3dddi_multiplane_overlay_video_frame_format)|オーバーレイ平面のビデオ フレームの形式を識別します。 D3DDDI_MULTIPLANE_OVERLAY_VIDEO_FRAME_FORMAT_PROGRESSIVE 値のみがサポートされています。|
|[D3DDDI_MULTIPLANE_OVERLAY_YCbCr_FLAGS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ne-d3dumddi-d3dddi_multiplane_overlay_ycbcr_flags)| Multiplane オーバーレイをについて説明します。 YUV の範囲と変換の情報を識別します。|
|[D3DDDI_PRESENT_MULTIPLANE_OVERLAY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddi_present_multiplane_overlay)| オーバーレイを表示するプレーンを指定します。|
|[D3DDDIARG_CHECKMULTIPLANEOVERLAYSUPPORT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_checkmultiplaneoverlaysupport)| PfnCheckMultiPlaneOverlaySupport (D3D) 関数の呼び出しで multiplane オーバーレイのハードウェア サポートの詳細を確認するために使用します。|
|[D3DDDIARG_PRESENTMULTIPLANEOVERLAY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-d3dddiarg_presentmultiplaneoverlay)| Multiplane オーバーレイを表示するリソースを指定します。|
|[D3DDDICB_PRESENTMULTIPLANEOVERLAY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-d3dddicb_presentmultiplaneoverlay)| 間にコンテンツがコピーされる multiplane オーバーレイの割り当てについて説明します。|
 
## <a name="multiplane-overlay-kernel-mode-driver-implemented-functions"></a>Multiplane オーバーレイのカーネル モード ドライバー実装関数

ディスプレイのミニポート ドライバーを実装するすべての multiplane オーバーレイ関数。

|関数|説明|
|:--|:--|
|[DXGKDDI_CHECKMULTIPLANEOVERLAYSUPPORT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_checkmultiplaneoverlaysupport)| Multiplane オーバーレイ用ハードウェア サポートの詳細を確認するには、Microsoft DirectX グラフィックス カーネル サブシステムによって呼び出されます。|
|[DXGKDDI_CHECKMULTIPLANEOVERLAYSUPPORT3](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_checkmultiplaneoverlaysupport3)| 次の新しい関数は、特定のプレーン マルチ オーバーレイ構成がサポートされているかどうかを判断すると呼ばれます。|
|[DXGKDDI_GETMULTIPLANEOVERLAYCAPS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_getmultiplaneoverlaycaps)| 呼ばれる multiplane を取得するオーバーレイ機能をします。 この DDI は複数の面をサポートする WDDM 2.2 ドライバーに必要なサポートします。|
|[DXGKDDI_POSTMULTIPLANEOVERLAYPRESENT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_postmultiplaneoverlaypresent)| 新しいマルチ プレーン オーバーレイ構成がハードウェアの状態を最適化するためにドライバーを許可する効果を取得後に呼び出されます。 マルチ プレーン オーバーレイをサポートする Windows Display Driver Model (WDDM) 2.0 以降ドライバーに対して省略可能です。|
|[DXGKDDI_SETVIDPNSOURCEADDRESSWITHMULTIPLANEOVERLAY3](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_setvidpnsourceaddresswithmultiplaneoverlay3)|表示されるオーバーレイの構成を変更するには、呼び出されます。|
|[DXGKDDI_CHECKMULTIPLANEOVERLAYSUPPORT2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_checkmultiplaneoverlaysupport2)|特定のプレーン マルチ オーバーレイ構成がサポートされているかどうかを判断する DxgkDdiCheckMultiPlaneOverlaySupport2 と呼びます。 |
|[DXGKDDI_SETVIDPNSOURCEADDRESSWITHMULTIPLANEOVERLAY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_setvidpnsourceaddresswithmultiplaneoverlay)|特定のビデオ存在するソースに関連付けられた複数のサーフェスのデスクトップ ウィンドウ マネージャー (DWM) のスワップなどのアドレスを設定します。 この関数は、画面に複数のサーフェス (DWM のスワップを含む) を提示する使用されます。|
|[DXGKDDI_SETVIDPNSOURCEADDRESSWITHMULTIPLANEOVERLAY2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_setvidpnsourceaddresswithmultiplaneoverlay2)| DxgkDdiSetVidPnSourceAddressWithMultiPlaneOverlay2 が表示されるオーバーレイの構成を変更すると呼ばれます。|

## <a name="multiplane-overlay-kernel-mode-structures"></a>Multiplane オーバーレイ カーネル モードの構造体

ディスプレイのミニポート ドライバーで使用されるすべての構造体。

|構造体|説明|
|:--|:--|
|[DXGK_CHECK_MULTIPLANE_OVERLAY_SUPPORT_PLANE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_check_multiplane_overlay_support_plane)| Multiplane オーバーレイのハードウェアを提供するサポートの属性を指定します。|
|[DXGK_CHECK_MULTIPLANE_OVERLAY_SUPPORT_RETURN_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-dxgk_check_multiplane_overlay_support_return_info)| Multiplane オーバーレイのハードウェア サポートの制限を指定します。|
|[DXGK_MULTIPLANE_OVERLAY_ATTRIBUTES](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_multiplane_overlay_attributes)| ディスプレイのミニポート ドライバーによってオーバーレイ平面の属性を指定するために使用します。|
|[DXGK_MULTIPLANE_OVERLAY_ATTRIBUTES2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_multiplane_overlay_attributes2)|DXGK_MULTIPLANE_OVERLAY_ATTRIBUTES2 は、オーバーレイ平面の属性を指定するディスプレイのミニポート ドライバーによって使用されます。 |
|[DXGK_MULTIPLANE_OVERLAY_BLEND](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_multiplane_overlay_blend)| オーバーレイ平面に実行する合成操作を識別します。|
|[DXGK_MULTIPLANE_OVERLAY_FLAGS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_multiplane_overlay_flags)| オーバーレイ平面に実行する反転操作を識別します。|
|[DXGK_MULTIPLANE_OVERLAY_PLANE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_multiplane_overlay_plane)| オーバーレイ プレーン DxgkDdiSetVidPnSourceAddressWithMultiPlaneOverlay 関数の呼び出しに表示するを指定します。|
|[DXGK_MULTIPLANE_OVERLAY_PLANE2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_multiplane_overlay_plane2)|DXGK_MULTIPLANE_OVERLAY_PLANE2 は、オーバーレイを表示するプレーンを指定する DxgkDdiSetVidPnSourceAddressWithMultiPlaneOverlay2 関数と共に使用されます。|
|[DXGK_MULTIPLANE_OVERLAY_PLANE_WITH_SOURCE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_multiplane_overlay_plane_with_source)|DXGK_MULTIPLANE_OVERLAY_PLANE_WITH_SOURCE には、マルチ プレーン オーバーレイ平面属性、割り当て、およびビデオの存在するネットワーク ソースの識別番号がについて説明します。|
|[DXGK_MULTIPLANE_OVERLAY_VSYNC_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_multiplane_overlay_vsync_info)|垂直同期の間隔中に表示する、オーバーレイの平面を指定します。|
|[DXGK_MULTIPLANE_OVERLAY_YCbCr_FLAGS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_multiplane_overlay_ycbcr_flags)|Multiplane オーバーレイをについて説明します。 YUV の範囲と変換の情報を識別します。|
|[DXGK_PRESENTMULTIPLANEOVERLAYINFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_presentmultiplaneoverlayinfo)|VidPN 入力し、オーバーレイの面を表示する情報を指定します。|
|[DXGK_PRESENTMULTIPLANEOVERLAYLIST](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_presentmultiplaneoverlaylist)|オーバーレイ プレーン DxgkDdiPresent 関数の呼び出しに表示するを指定します。|
|[DXGKARG_CHECKMULTIPLANEOVERLAYSUPPORT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_checkmultiplaneoverlaysupport)|DxgkDdiCheckMultiPlaneOverlaySupport 関数の呼び出しで multiplane オーバーレイのハードウェア サポートの詳細を確認するために使用します。|
|[DXGKARG_CHECKMULTIPLANEOVERLAYSUPPORT2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_checkmultiplaneoverlaysupport2)|DXGKARG_CHECKMULTIPLANEOVERLAYSUPPORT2 は、特定のプレーン マルチ オーバーレイ構成がサポートされているかどうかを決定する DxgkDdiCheckMultiPlaneOverlaySupport2 関数に渡されます。|
|[DXGKARG_SETVIDPNSOURCEADDRESSWITHMULTIPLANEOVERLAY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_setvidpnsourceaddresswithmultiplaneoverlay)|DxgkDdiSetVidPnSourceAddressWithMultiPlaneOverlay 関数の引数が含まれています。|
|[DXGKARG_SETVIDPNSOURCEADDRESSWITHMULTIPLANEOVERLAY2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_setvidpnsourceaddresswithmultiplaneoverlay2)|DXGKARG_SETVIDPNSOURCEADDRESSWITHMULTIPLANEOVERLAY2 は、表示されるオーバーレイの構成を変更する DxgkDdiSetVidPnSourceAddressWithMultiPlaneOverlay2 関数に渡されます。|
 

## <a name="multiplane-overlay-kernel-mode-enumerations"></a>Multiplane オーバーレイ カーネル モードの列挙型

ディスプレイのミニポート ドライバーで使用されるすべての列挙体。

| 列挙値 | 説明 |
|:--|:--|
|[DXGK_MULTIPLANE_OVERLAY_STEREO_FLIP_MODE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ne-d3dkmddi-_dxgk_multiplane_overlay_stereo_flip_mode)|オーバーレイ平面のステレオ フリップ モードを識別します。 DXGK_MULTIPLANE_OVERLAY_STEREO_FLIP_NONE 値のみがサポートされています。 |
|[DXGK_MULTIPLANE_OVERLAY_STEREO_FORMAT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ne-d3dkmddi-_dxgk_multiplane_overlay_stereo_format)|オーバーレイ平面のステレオの表示形式を識別します。 DXGK_MULTIPLANE_OVERLAY_STEREO_FORMAT_MONO 値のみがサポートされています。|
|[DXGK_MULTIPLANE_OVERLAY_STRETCH_QUALITY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ne-d3dkmddi-_dxgk_multiplane_overlay_stretch_quality)|ハードウェアが拡大または multiplane オーバーレイ データを圧縮するときに実行する必要がありますフィルタ リングのプロセスを識別します。|
|[DXGK_MULTIPLANE_OVERLAY_VIDEO_FRAME_FORMAT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ne-d3dkmddi-_dxgk_multiplane_overlay_video_frame_format)|オーバーレイ平面のビデオ フレームの形式を識別します。 DXGK_MULTIPLANE_OVERLAY_VIDEO_FRAME_FORMAT_PROGRESSIVE 値のみがサポートされています。|
 

このユーザー モードの列挙定数の値は、multiplane オーバーレイをサポートしているし、は、Windows 8.1 の新機能。

-   [**D3DDDICAPS\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ne-d3dumddi-_d3dddicaps_type) (**D3DDDICAPS\_取得\_MULTIPLANE\_オーバーレイ\_グループ\_CAP**定数値)

 

 





