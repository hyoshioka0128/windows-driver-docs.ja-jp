---
title: ビデオ処理の機能の提供
description: ビデオ処理の機能の提供
ms.assetid: 27507971-1545-44d9-885a-295b9357bdfe
keywords:
- ビデオ処理 WDK DirectX VA、要求の種類によって提供される機能
- D3DDDICAPS_GETVIDEOPROCESSORDEVICEGUIDCOUNT
- D3DDDICAPS_GETVIDEOPROCESSORDEVICEGUIDS
- D3DDDICAPS_GETVIDEOPROCESSORCAPS
- D3DDDICAPS_GETPROCAMPRANGE
- D3DDDICAPS_GETVIDEOPROCESSORRTFORMATCOUNT
- D3DDDICAPS_GETVIDEOPROCESSORRTFORMATS
- D3DDDICAPS_GETVIDEOPROCESSORRTSUBSTREAMFORMATCOUNT
- D3DDDICAPS_GETVIDEOPROCESSORRTSUBSTREAMFORMATS
- D3DDDICAPS_FILTERPROPERTYRANGE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ca61e7b2319fdb670d52694650d2acb747557cf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826016"
---
# <a name="providing-capabilities-for-video-processing"></a>ビデオ処理の機能の提供


[**Getcaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps)関数が呼び出されると、ユーザーモード表示ドライバーは、要求の種類に基づいて次のビデオ処理機能を提供します ( [**D3DDDIARG\_getcaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)構造体の**type**メンバーで指定されています)。*pData*パラメーターが指す):

<span id="D3DDDICAPS_GETVIDEOPROCESSORDEVICEGUIDCOUNT_and_D3DDDICAPS_GETVIDEOPROCESSORDEVICEGUIDS_request_types"></span><span id="d3dddicaps_getvideoprocessordeviceguidcount_and_d3dddicaps_getvideoprocessordeviceguids_request_types"></span><span id="D3DDDICAPS_GETVIDEOPROCESSORDEVICEGUIDCOUNT_AND_D3DDDICAPS_GETVIDEOPROCESSORDEVICEGUIDS_REQUEST_TYPES"></span>D3DDDICAPS\_GETVIDEOPROCESSORDEVICEGUIDCOUNT と D3DDDICAPS\_GETVIDEOPROCESSORDEVICEGUID 要求の種類  
ユーザーモード表示ドライバーは、ビデオ処理に対してサポートされている次の Guid の番号とリストを返します。 Microsoft Direct3D ランタイムは、D3DDDIARG\_GETCAPS**が指す**変数で処理する特定のビデオストリームの[**DXVADDI\_videodesc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvaddi_videodesc)構造を指定します。 ランタイムはまず、サポートされている Guid の数を要求し、次にサポートされている Guid の一覧を要求します。

```cpp
DEFINE_GUID(DXVADDI_VideoProcProgressiveDevice,  0x5a54a0c9,0xc7ec,0x4bd9,0x8e,0xde,0xf3,0xc7,0x5d,0xc4,0x39,0x3b);
DEFINE_GUID(DXVADDI_VideoProcBobDevice,  0x335aa36e,0x7884,0x43a4,0x9c,0x91,0x7f,0x87,0xfa,0xf3,0xe3,0x7e);
```

<span id="D3DDDICAPS_GETVIDEOPROCESSORCAPS_request_type"></span><span id="d3dddicaps_getvideoprocessorcaps_request_type"></span><span id="D3DDDICAPS_GETVIDEOPROCESSORCAPS_REQUEST_TYPE"></span>D3DDDICAPS\_GETVIDEOPROCESSORCAPS 要求の種類  
ユーザーモードディスプレイドライバーでサポートされている各ビデオプロセッサモードは、固有の機能を持つことができます。 ユーザーモードの表示ドライバーは、D3DDDICAPS\_GETVIDEOPROCESSORCAPS 要求の種類が渡されたときにこれらの機能を返します。 Direct3D ランタイムは、ビデオ処理モードの[**DXVADDI\_VIDEOPROCESSORINPUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvaddi_videoprocessorinput)構造体を指定して、 [**D3DDDIARG\_Getcaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)が指すの**pInfo**メンバーが指す変数内のの機能を取得します。 ユーザーモード表示ドライバーは、\_D3DDDIARG の**pData**メンバーが指す[**DXVADDI\_videoprocessorcaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvaddi_videoprocessorcaps)構造体のビデオ処理モードの機能を返します。

<span id="D3DDDICAPS_GETPROCAMPRANGE_request_type_"></span><span id="d3dddicaps_getprocamprange_request_type_"></span><span id="D3DDDICAPS_GETPROCAMPRANGE_REQUEST_TYPE_"></span>D3DDDICAPS\_GETPROCAMPRANGE 要求の種類   
ユーザーモード表示ドライバーは、特定のビデオストリームの特定の ProcAmp コントロールプロパティに許可されている値の範囲を含む[**DXVADDI\_VALUERANGE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvaddi_valuerange)構造体へのポインターを返します。 Direct3D ランタイムは、D3DDDIARG\_GETCAPS が指し示す**pInfo**メンバーが指す変数内の特定のビデオストリームの ProcAmp コントロールプロパティに、 [**DXVADDI\_QUERYPROCAMPINPUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvaddi_queryprocampinput)構造体を指定します。

<span id="D3DDDICAPS_GETVIDEOPROCESSORRTFORMATCOUNT_and_D3DDDICAPS_GETVIDEOPROCESSORRTFORMATS_request_types"></span><span id="d3dddicaps_getvideoprocessorrtformatcount_and_d3dddicaps_getvideoprocessorrtformats_request_types"></span><span id="D3DDDICAPS_GETVIDEOPROCESSORRTFORMATCOUNT_AND_D3DDDICAPS_GETVIDEOPROCESSORRTFORMATS_REQUEST_TYPES"></span>D3DDDICAPS\_GETVIDEOPROCESSORRTFORMATCOUNT および D3DDDICAPS\_GETVIDEOPROCESSORRTFORMATS 要求の種類  
ユーザーモード表示ドライバーは、特定のビデオ処理モードでサポートされているレンダーターゲット形式の数とリストを返します。 Direct3D ランタイムは、D3DDDIARG\_GETCAPS**が指す**変数のビデオプロセッサモードに対して、 [**DXVADDI\_videoprocessorinput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvaddi_videoprocessorinput)構造体を指定します。 ユーザーモード表示ドライバーは、 [**D3DDDIFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ne-d3dukmdt-_d3dddiformat)型の値の配列でサポートされているレンダーターゲット形式を返します。この形式は、D3DDDIARG\_Getcaps の**pData**メンバーによって指定されます。

<span id="D3DDDICAPS_GETVIDEOPROCESSORRTSUBSTREAMFORMATCOUNT_and_D3DDDICAPS_GETVIDEOPROCESSORRTSUBSTREAMFORMATS_request_types"></span><span id="d3dddicaps_getvideoprocessorrtsubstreamformatcount_and_d3dddicaps_getvideoprocessorrtsubstreamformats_request_types"></span><span id="D3DDDICAPS_GETVIDEOPROCESSORRTSUBSTREAMFORMATCOUNT_AND_D3DDDICAPS_GETVIDEOPROCESSORRTSUBSTREAMFORMATS_REQUEST_TYPES"></span>D3DDDICAPS\_GETVIDEOPROCESSORRTSUBSTREAMFORMATCOUNT および D3DDDICAPS\_GETVIDEOPROCESSORRTSUBSTREAMFORMATS 要求の種類  
ユーザーモード表示ドライバーは、特定のビデオ処理モードでサポートされているサブストリーム形式の番号と一覧を返します。 Direct3D ランタイムは、D3DDDIARG\_GETCAPS**が指す**変数のビデオプロセッサモードに対して、 [**DXVADDI\_videoprocessorinput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvaddi_videoprocessorinput)構造体を指定します。 ユーザーモード表示ドライバーは、 [**D3DDDIFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ne-d3dukmdt-_d3dddiformat)型の値の配列でサポートされているサブストリーム形式を返します。この形式は、D3DDDIARG\_Getcaps の**pData**メンバーによって指定されます。

<span id="D3DDDICAPS_FILTERPROPERTYRANGE_request_type_"></span><span id="d3dddicaps_filterpropertyrange_request_type_"></span><span id="D3DDDICAPS_FILTERPROPERTYRANGE_REQUEST_TYPE_"></span>D3DDDICAPS\_FILTERPROPERTYRANGE 要求の種類   
ユーザーモード表示ドライバーは、D3DDDICAPS\_FILTERPROPERTYRANGE 要求がある場合に、特定のビデオストリームの特定のフィルター設定で許容される値の範囲を含む[**DXVADDI\_VALUERANGE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvaddi_valuerange)構造体へのポインターを返します。型が渡されます。 Direct3D ランタイムは、D3DDDIARG\_GETCAPS**が指す**変数内の特定のビデオストリームに対して、フィルター設定の[**DXVADDI\_QUERYFILTERPROPERTYRANGEINPUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvaddi_queryfilterpropertyrangeinput)構造を指定します。

 

 





