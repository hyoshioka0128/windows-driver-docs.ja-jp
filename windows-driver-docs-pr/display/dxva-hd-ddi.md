---
title: DXVA-HD DDI
description: DXVA-HD DDI
ms.assetid: 8b44a5b7-dc86-46eb-83e1-39caa72ffa34
keywords:
- DXVA-HD DDI WDK Windows 7 ディスプレイ
- DXVA-HD DDI WDK Server 2008 R2 ディスプレイ
- 高解像度ビデオ WDK Windows 7 display、DXVA-HD DDI
- 高解像度ビデオ WDK Server 2008 R2 display, DXVA-HD DDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b5a763b0978588c28a2e9e4b8e65096e89c70d8e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838962"
---
# <a name="dxva-hd-ddi"></a>DXVA-HD DDI


このセクションは、windows 7 以降、および windows Server 2008 R2 以降のバージョンの Windows オペレーティングシステムにのみ適用されます。

DXVA-HD DDI は、高解像度ビデオの処理を処理する[Direct3D バージョン 9 DDI](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/index)の拡張機能です。 DXVA-HD DDI は、次のエントリポイントで構成されています。

-   次の[**D3DDDICAPS\_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-_d3dddicaps_type)値は、ユーザーモードディスプレイドライバーがサポートする高解像度のビデオ処理機能に関する情報を取得するために、Direct3D ランタイムによって使用されます。 ランタイムは、このような**D3DDDICAPS\_型**の値を、 [**D3DDDIARG\_getcaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)構造体の型のメンバーに設定します。この**型**の値は、ドライバーの[**getcaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps)関数の*pData*パラメーターがを呼び出したときに、*Getcaps*。

    <span id="D3DDDICAPS_DXVAHD_GETVPDEVCAPS"></span><span id="d3dddicaps_dxvahd_getvpdevcaps"></span>D3DDDICAPS\_DXVAHD\_GETVPDEVCAPS  
    ドライバーは、デコードデバイス ( [**DXVAHDDDI\_デバイス\_DESC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvahdddi_device_desc)構造体に指定されて**いる、** [**D3DDDIARG\_getcaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)) がサポートしているビデオプロセッサ機能の[**DXVAHDDDI\_vpdevcaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvahdddi_vpdevcaps)構造体へのポインターを提供します。

    <span id="D3DDDICAPS_DXVAHD_GETVPOUTPUTFORMATS"></span><span id="d3dddicaps_dxvahd_getvpoutputformats"></span>D3DDDICAPS\_DXVAHD\_GETVPOUTPUTFORMATS  
    ドライバーは、デコードデバイスの出力形式を表す[**D3DDDIFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ne-d3dukmdt-_d3dddiformat)列挙型の配列を提供します。これは、 **pInfo**メンバーによってポイントされる[**DXVAHDDDI\_デバイス\_DESC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvahdddi_device_desc)構造体で指定されています。[**D3DDDIARG\_GETCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps))。

    <span id="D3DDDICAPS_DXVAHD_GETVPINPUTFORMATS"></span><span id="d3dddicaps_dxvahd_getvpinputformats"></span>D3DDDICAPS\_DXVAHD\_GETVPINPUTFORMATS  
    ドライバーは、デコードデバイスの入力形式を表す[**D3DDDIFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ne-d3dukmdt-_d3dddiformat)列挙型の配列を提供します。これは、 **pInfo**メンバーによってポイントされる[**DXVAHDDDI\_デバイス\_DESC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvahdddi_device_desc)構造体で指定されています。[**D3DDDIARG\_GETCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps))。

    <span id="D3DDDICAPS_DXVAHD_GETVPCAPS"></span><span id="d3dddicaps_dxvahd_getvpcaps"></span>D3DDDICAPS\_DXVAHD\_GETVPCAPS  
    ドライバーは、デコードデバイス ( [**DXVAHDDDI\_デバイス\_DESC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvahdddi_device_desc)構造体に指定されている各ビデオプロセッサの機能に対して、 [**DXVAHDDDI\_vpcaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvahdddi_vpcaps)構造体の配列を提供します。これは、[**D3DDDIARG\_GETCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)) の**pInfo**メンバーは、をサポートしています。

    <span id="D3DDDICAPS_DXVAHD_GETVPCUSTOMRATES"></span><span id="d3dddicaps_dxvahd_getvpcustomrates"></span>D3DDDICAPS\_DXVAHD\_GETVPCUSTOMRATES  
    このドライバーは、ビデオプロセッサ ( [**D3DDDIARG\_GETCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)の**pInfo**メンバーによってポイントされている CONST\_GUID によって指定される) がサポートしているカスタムフレームレートの[**データ構造\_、DXVAHDDDI\_カスタム\_レート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvahdddi_custom_rate_data)の配列を提供します。

    <span id="D3DDDICAPS_DXVAHD_GETVPFILTERRANGE"></span><span id="d3dddicaps_dxvahd_getvpfilterrange"></span>D3DDDICAPS\_DXVAHD\_GETVPFILTERRANGE  
    ドライバーは、フィルターによって指定されている範囲[ **\_\_範囲の DXVAHDDDI\_フィルター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvahdddi_filter_range_data)にポインターを提供します (これは、 **pInfo**によってポイントされるフィルター列挙値[ **\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-_dxvahdddi_filter)によって指定されます)。[**D3DDDIARG\_GETCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)) のメンバーは、をサポートしています。

-   [**Createvideoprocessor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_dxvahd_createvideoprocessor)関数は、高解像度ビデオを処理できるビデオプロセッサを作成します。

-   [**SetVideoProcessBltState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_dxvahd_setvideoprocessbltstate)関数は、ビデオプロセッサのビットブロック転送 (bitblt) の状態を設定します。

-   [**Getvideoprocessbltstateprivate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_dxvahd_getvideoprocessbltstateprivate)関数は、ビデオプロセッサのプライベート bitblt の状態データを取得します。

-   [**Setvideoprocessstreamstate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_dxvahd_setvideoprocessstreamstate)関数は、ビデオプロセッサのストリームの状態を設定します。

-   [**Getvideoprocessstreamstateprivate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_dxvahd_getvideoprocessstreamstateprivate)関数は、ビデオプロセッサのプライベートストリーム状態データを取得します。

-   [**Videoprocessblthd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_dxvahd_videoprocessblthd)関数は、ビデオ入力ストリームを処理し、出力サーフェイスに合成します。

-   [**Destroyvideoprocessor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_dxvahd_destroyvideoprocessor)関数は、以前に作成されたビデオプロセッサのリソースを解放します。

 

 





