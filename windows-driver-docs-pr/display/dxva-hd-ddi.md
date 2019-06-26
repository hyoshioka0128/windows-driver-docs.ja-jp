---
title: DXVA-HD DDI
description: DXVA-HD DDI
ms.assetid: 8b44a5b7-dc86-46eb-83e1-39caa72ffa34
keywords:
- DXVA HD DDI WDK Windows 7 の表示
- DXVA HD DDI WDK Server 2008 R2 の表示
- 高解像度ビデオ Windows 7 の WDK ディスプレイ、DXVA HD DDI
- 高解像度ビデオ WDK Server 2008 R2 ディスプレイ、DXVA HD DDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c8b31fe8ce47ddb1aadebaf80332fc0a1a9d9046
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375836"
---
# <a name="dxva-hd-ddi"></a>DXVA-HD DDI


このセクションでは、Windows 7 以降および Windows Server 2008 R2 以降のバージョンの Windows オペレーティング システムにのみ適用されます。

DXVA HD DDI は拡張機能、 [Direct3D のバージョン 9 DDI](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/index)高解像度ビデオの処理を処理します。 DXVA HD DDI は、次のエントリ ポイントで構成されます。

-   次[ **D3DDDICAPS\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ne-d3dumddi-_d3dddicaps_type)値は、ユーザー モードで表示する高解像度ビデオの処理機能についての情報を取得する Direct3D のランタイムによって使用されますドライバーをサポートします。 ランタイム設定**D3DDDICAPS\_型**値、**型**のメンバー、 [ **D3DDDIARG\_GETCAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)構造体、 *pData*のドライバーのパラメーター [ **GetCaps** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps)関数ランタイムが呼び出すときに指す*GetCaps*.

    <span id="D3DDDICAPS_DXVAHD_GETVPDEVCAPS"></span><span id="d3dddicaps_dxvahd_getvpdevcaps"></span>D3DDDICAPS\_DXVAHD\_GETVPDEVCAPS  
    ドライバーへのポインターを提供する、 [ **DXVAHDDDI\_VPDEVCAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_dxvahdddi_vpdevcaps)ビデオ プロセッサの機能の構造をデコード デバイス (で指定される、 [ **DXVAHDDDI\_デバイス\_DESC** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_dxvahdddi_device_desc)が指す構造、 **pInfo**のメンバー [ **D3DDDIARG\_GETCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)) をサポートしています。

    <span id="D3DDDICAPS_DXVAHD_GETVPOUTPUTFORMATS"></span><span id="d3dddicaps_dxvahd_getvpoutputformats"></span>D3DDDICAPS\_DXVAHD\_GETVPOUTPUTFORMATS  
    ドライバーの配列を提供する[ **D3DDDIFORMAT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ne-d3dukmdt-_d3dddiformat)デコード デバイスの出力形式を表す列挙型 (で指定される、 [ **DXVAHDDDI\_デバイス\_DESC** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_dxvahdddi_device_desc)が指す構造、 **pInfo**のメンバー [ **D3DDDIARG\_GETCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)).

    <span id="D3DDDICAPS_DXVAHD_GETVPINPUTFORMATS"></span><span id="d3dddicaps_dxvahd_getvpinputformats"></span>D3DDDICAPS\_DXVAHD\_GETVPINPUTFORMATS  
    ドライバーの配列を提供する[ **D3DDDIFORMAT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ne-d3dukmdt-_d3dddiformat)デコード デバイスの入力の形式を表す列挙型 (で指定される、 [ **DXVAHDDDI\_デバイス\_DESC** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_dxvahdddi_device_desc)が指す構造、 **pInfo**のメンバー [ **D3DDDIARG\_GETCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)).

    <span id="D3DDDICAPS_DXVAHD_GETVPCAPS"></span><span id="d3dddicaps_dxvahd_getvpcaps"></span>D3DDDICAPS\_DXVAHD\_GETVPCAPS  
    ドライバーの配列を提供する[ **DXVAHDDDI\_VPCAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_dxvahdddi_vpcaps)ビデオ プロセッサごとの機能の構造をデコード デバイス (で指定される、 [ **DXVAHDDDI\_デバイス\_DESC** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_dxvahdddi_device_desc)が指す構造、 **pInfo**のメンバー [ **D3DDDIARG\_GETCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)) をサポートしています。

    <span id="D3DDDICAPS_DXVAHD_GETVPCUSTOMRATES"></span><span id="d3dddicaps_dxvahd_getvpcustomrates"></span>D3DDDICAPS\_DXVAHD\_GETVPCUSTOMRATES  
    ドライバーの配列を提供します[ **DXVAHDDDI\_カスタム\_レート\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_dxvahdddi_custom_rate_data)構造体のカスタムのフレーム レートのビデオのプロセッサ (指定されている、CONST\_を指しています GUID、 **pInfo**のメンバー [ **D3DDDIARG\_GETCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)) をサポートしています。

    <span id="D3DDDICAPS_DXVAHD_GETVPFILTERRANGE"></span><span id="d3dddicaps_dxvahd_getvpfilterrange"></span>D3DDDICAPS\_DXVAHD\_GETVPFILTERRANGE  
    ドライバーへのポインターを提供する、 [ **DXVAHDDDI\_フィルター\_範囲\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_dxvahdddi_filter_range_data)範囲の構造体をフィルター (、で指定される[ **DXVAHDDDI\_フィルター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ne-d3dumddi-_dxvahdddi_filter)を指しています列挙値、 **pInfo**のメンバー [ **D3DDDIARG\_GETCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)) をサポートしています。

-   [ **CreateVideoProcessor** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_dxvahd_createvideoprocessor)関数は、高解像度ビデオを処理できるビデオ プロセッサを作成します。

-   [ **SetVideoProcessBltState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_dxvahd_setvideoprocessbltstate)関数は、ビデオのプロセッサのビット ブロック転送 (bitblt) の状態を設定します。

-   [ **GetVideoProcessBltStatePrivate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_dxvahd_getvideoprocessbltstateprivate)関数は、ビデオのプロセッサのプライベート bitblt の状態データを取得します。

-   [ **SetVideoProcessStreamState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_dxvahd_setvideoprocessstreamstate)関数は、ビデオのプロセッサのストリームの状態を設定します。

-   [ **GetVideoProcessStreamStatePrivate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_dxvahd_getvideoprocessstreamstateprivate)関数は、ビデオのプロセッサのプライベートのストリームの状態データを取得します。

-   [ **VideoProcessBltHD** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_dxvahd_videoprocessblthd)関数は、ビデオの入力ストリームを処理し、出力を画面に合成します。

-   [ **DestroyVideoProcessor** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_dxvahd_destroyvideoprocessor)関数は、以前に作成したビデオのプロセッサ リソースを解放します。

 

 





