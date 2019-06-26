---
title: ビデオ処理の機能の提供
description: ビデオ処理の機能の提供
ms.assetid: 27507971-1545-44d9-885a-295b9357bdfe
keywords:
- ビデオ処理 WDK DirectX va なので、要求の種類によって提供される機能
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
ms.openlocfilehash: 72e4cd2d5a35efb1704fcb9239cdc0eda1795f5d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383905"
---
# <a name="providing-capabilities-for-video-processing"></a>ビデオ処理の機能の提供


ときにその[ **GetCaps** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps)関数が呼び出されると、ユーザー モードのディスプレイ ドライバーが、要求の種類に基づいて次のビデオの処理機能を提供します (で指定される、 **の種類**のメンバー、 [ **D3DDDIARG\_GETCAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)構造体、 *pData*パラメーターが指す)。

<span id="D3DDDICAPS_GETVIDEOPROCESSORDEVICEGUIDCOUNT_and_D3DDDICAPS_GETVIDEOPROCESSORDEVICEGUIDS_request_types"></span><span id="d3dddicaps_getvideoprocessordeviceguidcount_and_d3dddicaps_getvideoprocessordeviceguids_request_types"></span><span id="D3DDDICAPS_GETVIDEOPROCESSORDEVICEGUIDCOUNT_AND_D3DDDICAPS_GETVIDEOPROCESSORDEVICEGUIDS_REQUEST_TYPES"></span>D3DDDICAPS\_GETVIDEOPROCESSORDEVICEGUIDCOUNT と D3DDDICAPS\_GETVIDEOPROCESSORDEVICEGUIDS 要求の種類  
ユーザー モードのディスプレイ ドライバーは、数とビデオの処理をサポートしている次の Guid のリストを返します。 マイクロソフトの Direct3D ランタイムを指定します、 [ **DXVADDI\_VIDEODESC** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_dxvaddi_videodesc)変数で処理する特定のビデオ ストリームの構造を**pInfo**メンバーの D3DDDIARG\_GETCAPS が指します。 ランタイムは、まずサポートされている Guid の後にサポートされている Guid の一覧については、要求の数を要求します。

```cpp
DEFINE_GUID(DXVADDI_VideoProcProgressiveDevice,  0x5a54a0c9,0xc7ec,0x4bd9,0x8e,0xde,0xf3,0xc7,0x5d,0xc4,0x39,0x3b);
DEFINE_GUID(DXVADDI_VideoProcBobDevice,  0x335aa36e,0x7884,0x43a4,0x9c,0x91,0x7f,0x87,0xfa,0xf3,0xe3,0x7e);
```

<span id="D3DDDICAPS_GETVIDEOPROCESSORCAPS_request_type"></span><span id="d3dddicaps_getvideoprocessorcaps_request_type"></span><span id="D3DDDICAPS_GETVIDEOPROCESSORCAPS_REQUEST_TYPE"></span>D3DDDICAPS\_GETVIDEOPROCESSORCAPS 要求の種類  
各ビデオ プロセッサ モード、ユーザー モードのディスプレイ ドライバーをサポートするには、固有の機能を持つことができます。 ユーザー モードのディスプレイ ドライバーがこれらの機能を返すときに、D3DDDICAPS\_GETVIDEOPROCESSORCAPS 要求の種類が渡されます。 Direct3D のランタイムを指定します、 [ **DXVADDI\_VIDEOPROCESSORINPUT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_dxvaddi_videoprocessorinput)変数の機能を取得するビデオ処理モードの構造を**pInfo**のメンバー [ **D3DDDIARG\_GETCAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)を指します。 ユーザー モードのディスプレイ ドライバーがビデオ処理モードの機能を返します、 [ **DXVADDI\_VIDEOPROCESSORCAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_dxvaddi_videoprocessorcaps)構造体、 **pData**メンバーの D3DDDIARG\_GETCAPS が指します。

<span id="D3DDDICAPS_GETPROCAMPRANGE_request_type_"></span><span id="d3dddicaps_getprocamprange_request_type_"></span><span id="D3DDDICAPS_GETPROCAMPRANGE_REQUEST_TYPE_"></span>D3DDDICAPS\_GETPROCAMPRANGE 要求の種類   
ユーザー モードのディスプレイ ドライバーへのポインターを返します、 [ **DXVADDI\_VALUERANGE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_dxvaddi_valuerange)の範囲を含む構造体では、特定の ProcAmp の特定のコントロール プロパティの値が許可されています。ビデオ ストリーム。 Direct3D のランタイムを指定します、 [ **DXVADDI\_QUERYPROCAMPINPUT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_dxvaddi_queryprocampinput) ProcAmp コントロール プロパティの変数に特定のビデオ ストリームの構造体を**pInfo** D3DDDIARG のメンバー\_GETCAPS を指します。

<span id="D3DDDICAPS_GETVIDEOPROCESSORRTFORMATCOUNT_and_D3DDDICAPS_GETVIDEOPROCESSORRTFORMATS_request_types"></span><span id="d3dddicaps_getvideoprocessorrtformatcount_and_d3dddicaps_getvideoprocessorrtformats_request_types"></span><span id="D3DDDICAPS_GETVIDEOPROCESSORRTFORMATCOUNT_AND_D3DDDICAPS_GETVIDEOPROCESSORRTFORMATS_REQUEST_TYPES"></span>D3DDDICAPS\_GETVIDEOPROCESSORRTFORMATCOUNT と D3DDDICAPS\_GETVIDEOPROCESSORRTFORMATS 要求の種類  
ユーザー モードでは、ドライバーの取得数と、一覧の表示、特定のビデオの処理モードをサポートしているターゲットの形式を表示します。 Direct3D のランタイムを指定します、 [ **DXVADDI\_VIDEOPROCESSORINPUT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_dxvaddi_videoprocessorinput)変数にビデオ プロセッサ モードの構造を**pInfo**のメンバーD3DDDIARG\_GETCAPS を指します。 ユーザー モードのディスプレイ ドライバー返しますレンダリング ターゲットの形式の配列でサポートされる[ **D3DDDIFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ne-d3dukmdt-_d3dddiformat)-型指定された値を**pData** D3DDDIARG のメンバー\_GETCAPS を指定します。

<span id="D3DDDICAPS_GETVIDEOPROCESSORRTSUBSTREAMFORMATCOUNT_and_D3DDDICAPS_GETVIDEOPROCESSORRTSUBSTREAMFORMATS_request_types"></span><span id="d3dddicaps_getvideoprocessorrtsubstreamformatcount_and_d3dddicaps_getvideoprocessorrtsubstreamformats_request_types"></span><span id="D3DDDICAPS_GETVIDEOPROCESSORRTSUBSTREAMFORMATCOUNT_AND_D3DDDICAPS_GETVIDEOPROCESSORRTSUBSTREAMFORMATS_REQUEST_TYPES"></span>D3DDDICAPS\_GETVIDEOPROCESSORRTSUBSTREAMFORMATCOUNT と D3DDDICAPS\_GETVIDEOPROCESSORRTSUBSTREAMFORMATS 要求の種類  
ユーザー モードは、数と、特定のビデオの処理モードをサポートしているサブ stream の形式の一覧に、ドライバーを返します。 を表示します。 Direct3D のランタイムを指定します、 [ **DXVADDI\_VIDEOPROCESSORINPUT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_dxvaddi_videoprocessorinput)変数にビデオ プロセッサ モードの構造を**pInfo**のメンバーD3DDDIARG\_GETCAPS を指します。 ユーザー モードのディスプレイ ドライバーの配列でサポートされているサブ stream の形式を返します[ **D3DDDIFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ne-d3dukmdt-_d3dddiformat)-型指定された値を**pData** D3DDDIARG のメンバー\_GETCAPS を指定します。

<span id="D3DDDICAPS_FILTERPROPERTYRANGE_request_type_"></span><span id="d3dddicaps_filterpropertyrange_request_type_"></span><span id="D3DDDICAPS_FILTERPROPERTYRANGE_REQUEST_TYPE_"></span>D3DDDICAPS\_FILTERPROPERTYRANGE 要求の種類   
ユーザー モードのディスプレイ ドライバーへのポインターを返します、 [ **DXVADDI\_VALUERANGE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_dxvaddi_valuerange)の範囲を含む構造体では、特定のビデオ ストリームで特定のフィルター設定の値が許可されています。ときに、D3DDDICAPS\_FILTERPROPERTYRANGE 要求の種類が渡されます。 Direct3D のランタイムを指定します、 [ **DXVADDI\_QUERYFILTERPROPERTYRANGEINPUT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_dxvaddi_queryfilterpropertyrangeinput)変数内の特定のビデオ ストリームのフィルター設定の構造を**pInfo** D3DDDIARG のメンバー\_GETCAPS を指します。

 

 





