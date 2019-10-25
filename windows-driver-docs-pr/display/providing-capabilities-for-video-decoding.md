---
title: ビデオ デコードの機能の提供
description: ビデオ デコードの機能の提供
ms.assetid: bffcc0da-7b1a-4f70-98f5-4841c8df9f12
keywords:
- ビデオデコード WDK DirectX VA、要求の種類ごとに提供される機能
- ビデオをデコードする WDK DirectX VA、要求の種類ごとに提供される機能
- D3DDDICAPS_GETDECODEGUIDCOUNT
- D3DDDICAPS_GETDECODEGUIDS
- D3DDDICAPS_GETDECODERTFORMATCOUNT
- D3DDDICAPS_GETDECODERTFORMATS
- D3DDDICAPS_GETDECODECOMPRESSEDBUFFERINFOCOUNT
- D3DDDICAPS_GETDECODECOMPRESSEDBUFFERINFO
- D3DDDICAPS_GETDECODECONFIGURATIONCOUNT
- D3DDDICAPS_GETDECODECONFIGURATIONS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 805bdcecd5a8806d70ca77d3401add29c2108baf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829673"
---
# <a name="providing-capabilities-for-video-decoding"></a>ビデオ デコードの機能の提供


[**Getcaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps)関数が呼び出されると、ユーザーモードの表示ドライバーは、要求の種類に基づいてビデオをデコードするための次の機能を提供します ( [**D3DDDIARG\_getcaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)構造体の**type**メンバーで指定されています)。*Getcaps*関数の*pData*パラメーターがを指す):

<span id="D3DDDICAPS_GETDECODEGUIDCOUNT_and_D3DDDICAPS_GETDECODEGUIDS_request_types"></span><span id="d3dddicaps_getdecodeguidcount_and_d3dddicaps_getdecodeguids_request_types"></span><span id="D3DDDICAPS_GETDECODEGUIDCOUNT_AND_D3DDDICAPS_GETDECODEGUIDS_REQUEST_TYPES"></span>D3DDDICAPS\_GETDECODEGUIDCOUNT および D3DDDICAPS\_GETDECODEGUIDS 要求の種類  
ユーザーモード表示ドライバーは、ビデオアクセラレーション (VA) のデコードでサポートされている次の Guid の番号と一覧を返します。 Microsoft Direct3D ランタイムは、最初に Guid の数を要求し、次にサポートされている Guid の一覧を要求します。

```cpp
DEFINE_GUID(DXVADDI_ModeMPEG2_MoComp, 0xe6a9f44b, 0x61b0, 0x4563,0x9e,0xa4,0x63,0xd2,0xa3,0xc6,0xfe,0x66);
DEFINE_GUID(DXVADDI_ModeMPEG2_IDCT,   0xbf22ad00, 0x03ea, 0x4690,0x80,0x77,0x47,0x33,0x46,0x20,0x9b,0x7e);
DEFINE_GUID(DXVADDI_ModeMPEG2_VLD,    0xee27417f, 0x5e28, 0x4e65,0xbe,0xea,0x1d,0x26,0xb5,0x08,0xad,0xc9);

DEFINE_GUID(DXVADDI_ModeH264_A,  0x1b81be64, 0xa0c7, 0x11d3,0xb9,0x84,0x00,0xc0,0x4f,0x2e,0x73,0xc5);
DEFINE_GUID(DXVADDI_ModeH264_B,  0x1b81be65, 0xa0c7, 0x11d3,0xb9,0x84,0x00,0xc0,0x4f,0x2e,0x73,0xc5);
DEFINE_GUID(DXVADDI_ModeH264_C,  0x1b81be66, 0xa0c7, 0x11d3,0xb9,0x84,0x00,0xc0,0x4f,0x2e,0x73,0xc5);
DEFINE_GUID(DXVADDI_ModeH264_D,  0x1b81be67, 0xa0c7, 0x11d3,0xb9,0x84,0x00,0xc0,0x4f,0x2e,0x73,0xc5);
DEFINE_GUID(DXVADDI_ModeH264_E,  0x1b81be68, 0xa0c7, 0x11d3,0xb9,0x84,0x00,0xc0,0x4f,0x2e,0x73,0xc5);
DEFINE_GUID(DXVADDI_ModeH264_F,  0x1b81be69, 0xa0c7, 0x11d3,0xb9,0x84,0x00,0xc0,0x4f,0x2e,0x73,0xc5);

DEFINE_GUID(DXVADDI_ModeWMV8_A,  0x1b81be80, 0xa0c7, 0x11d3,0xb9,0x84,0x00,0xc0,0x4f,0x2e,0x73,0xc5);
DEFINE_GUID(DXVADDI_ModeWMV8_B,  0x1b81be81, 0xa0c7, 0x11d3,0xb9,0x84,0x00,0xc0,0x4f,0x2e,0x73,0xc5);

DEFINE_GUID(DXVADDI_ModeWMV9_A,  0x1b81be90, 0xa0c7, 0x11d3,0xb9,0x84,0x00,0xc0,0x4f,0x2e,0x73,0xc5);
DEFINE_GUID(DXVADDI_ModeWMV9_B,  0x1b81be91, 0xa0c7, 0x11d3,0xb9,0x84,0x00,0xc0,0x4f,0x2e,0x73,0xc5);
DEFINE_GUID(DXVADDI_ModeWMV9_C,  0x1b81be94, 0xa0c7, 0x11d3,0xb9,0x84,0x00,0xc0,0x4f,0x2e,0x73,0xc5);

DEFINE_GUID(DXVADDI_ModeVC1_A,   0x1b81beA0, 0xa0c7, 0x11d3,0xb9,0x84,0x00,0xc0,0x4f,0x2e,0x73,0xc5);
DEFINE_GUID(DXVADDI_ModeVC1_B,   0x1b81beA1, 0xa0c7, 0x11d3,0xb9,0x84,0x00,0xc0,0x4f,0x2e,0x73,0xc5);
DEFINE_GUID(DXVADDI_ModeVC1_C,   0x1b81beA2, 0xa0c7, 0x11d3,0xb9,0x84,0x00,0xc0,0x4f,0x2e,0x73,0xc5);
DEFINE_GUID(DXVADDI_ModeVC1_D,   0x1b81beA3, 0xa0c7, 0x11d3,0xb9,0x84,0x00,0xc0,0x4f,0x2e,0x73,0xc5);

#define DXVADDI_ModeMPEG2_MOCOMP  DXVADDI_ModeMPEG2_MoComp

#define DXVADDI_ModeWMV8_PostProc  DXVADDI_ModeWMV8_A
#define DXVADDI_ModeWMV8_MoComp  DXVADDI_ModeWMV8_B

#define DXVADDI_ModeWMV9_PostProc  DXVADDI_ModeWMV9_A
#define DXVADDI_ModeWMV9_MoComp  DXVADDI_ModeWMV9_B
#define DXVADDI_ModeWMV9_IDCT  DXVADDI_ModeWMV9_C

#define DXVADDI_ModeVC1_PostProc  DXVADDI_ModeVC1_A
#define DXVADDI_ModeVC1_MoComp  DXVADDI_ModeVC1_B
#define DXVADDI_ModeVC1_IDCT  DXVADDI_ModeVC1_C
#define DXVADDI_ModeVC1_VLD  DXVADDI_ModeVC1_D

#define DXVADDI_ModeH264_MoComp_NoFGT  DXVADDI_ModeH264_A
#define DXVADDI_ModeH264_MoComp_FGT  DXVADDI_ModeH264_B
#define DXVADDI_ModeH264_IDCT_NoFGT  DXVADDI_ModeH264_C
#define DXVADDI_ModeH264_IDCT_FGT  DXVADDI_ModeH264_D
#define DXVADDI_ModeH264_VLD_NoFGT  DXVADDI_ModeH264_E
#define DXVADDI_ModeH264_VLD_FGT  DXVADDI_ModeH264_F
```

<span id="D3DDDICAPS_GETDECODERTFORMATCOUNT_and_D3DDDICAPS_GETDECODERTFORMATS_request_types"></span><span id="d3dddicaps_getdecodertformatcount_and_d3dddicaps_getdecodertformats_request_types"></span><span id="D3DDDICAPS_GETDECODERTFORMATCOUNT_AND_D3DDDICAPS_GETDECODERTFORMATS_REQUEST_TYPES"></span>D3DDDICAPS\_GETDECODERTFORMATCOUNT および D3DDDICAPS\_GETDECODERTFORMATS 要求の種類  
ユーザーモード表示ドライバーは、特定の DirectX VA デコードの種類に対してサポートされているレンダーターゲット形式の数とリストを返します。 Direct3D ランタイムは、 **pInfo**の[ **\_D3DDDIARG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)のメンバーが指す変数に、特定の DirectX VA デコードの種類の GUID を指定します。

<span id="D3DDDICAPS_GETDECODECOMPRESSEDBUFFERINFOCOUNT_and_D3DDDICAPS_GETDECODECOMPRESSEDBUFFERINFO_request_types"></span><span id="d3dddicaps_getdecodecompressedbufferinfocount_and_d3dddicaps_getdecodecompressedbufferinfo_request_types"></span><span id="D3DDDICAPS_GETDECODECOMPRESSEDBUFFERINFOCOUNT_AND_D3DDDICAPS_GETDECODECOMPRESSEDBUFFERINFO_REQUEST_TYPES"></span>D3DDDICAPS\_GETDECODECOMPRESSEDBUFFERINFOCOUNT および D3DDDICAPS\_GETDECODECOMPRESSEDBUFFERINFO 要求の種類  
ユーザーモード表示ドライバーは、ビデオのデコードを高速化するために必要な、圧縮されたバッファーの種類に関する情報と情報を返します。 Direct3D ランタイムは、D3DDDIARG\_GETCAPS が指し示す**pInfo**メンバーが指す変数に、特定の DirectX VA デコードの種類の[**DXVADDI\_DECODEINPUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvaddi_decodeinput)構造体を指定します。 ユーザーモードの表示ドライバーは、 [**DXVADDI\_DECODEBUFFERINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvaddi_decodebufferinfo)構造体の配列内の圧縮されたバッファーの種類に関する情報を返します。この構造体は、D3DDDIARG\_Getcaps の**pData**メンバーによって指定されます。

<span id="D3DDDICAPS_GETDECODECONFIGURATIONCOUNT_and_D3DDDICAPS_GETDECODECONFIGURATIONS_request_types"></span><span id="d3dddicaps_getdecodeconfigurationcount_and_d3dddicaps_getdecodeconfigurations_request_types"></span><span id="D3DDDICAPS_GETDECODECONFIGURATIONCOUNT_AND_D3DDDICAPS_GETDECODECONFIGURATIONS_REQUEST_TYPES"></span>D3DDDICAPS\_GETDECODECONFIGURATIONCOUNT および D3DDDICAPS\_GETDECODECONFIGURATIONS 要求の種類  
ユーザーモード表示ドライバーは、特定の DirectX VA デコードの種類に対してサポートされている、高速デコード構成の数とリストを返します。 Direct3D ランタイムは、D3DDDIARG\_GETCAPS が指し示す**pInfo**メンバーが指す変数に、特定の DirectX VA デコードの種類の DXVADDI\_DECODEINPUT 構造体を指定します。 ユーザーモードの表示ドライバーは、 [ **\_DXVADDI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvaddi_configpicturedecode)の配列内の高速デコード構成を返します。この構造は、D3DDDIARG\_Getcaps の**pData**メンバーによって指定されます。

 

 





