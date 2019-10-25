---
title: ピクセル形式の色の値の処理
description: ピクセル形式の色の値の処理
ms.assetid: 53ce6be1-14e1-4ee8-ba29-f198dcdacdaa
keywords:
- ピクセル形式の色の値 WDK DirectX 9.0
- ピクセル形式カラー値 WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95e0e7be16adcb2d0181f9ad6e90ef7a9b345b76
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839666"
---
# <a name="handling-color-values-for-pixel-formats"></a>ピクセル形式の色の値の処理


## <span id="ddk_handling_color_values_for_pixel_formats_gg"></span><span id="DDK_HANDLING_COLOR_VALUES_FOR_PIXEL_FORMATS_GG"></span>


**このトピックは、DirectX 7.0 以降に適用されます。**

アプリケーションでは、カラーフォーマットの ARGB クラスと YUV クラスの入力色の値を変換する必要があります。これは、これらの形式のサーフェイスでカラー塗りつぶしとクリア操作を一様に行う必要があるためです。 ただし、ドライバーは、他のクラス形式の色の値を直接使用する必要があります。 たとえば、アプリケーションは、アルファ (A)、赤 (R)、緑 (G)、および青 (B) の各コンポーネントに対して最大8ビットを持つすべてのサーフェイスの均一色の値として A8R8G8B8 を使用します。ドライバーは、最も重要度の高いビットをコピーすることによって、A8R8G8B8 の色を実際の ARGB 形式に固有の色の値に変換する必要があります。

ディスプレイドライバーは、 [**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)関数で D3DDP2OP\_CLEAR および D3DDP2OP\_colorfill 操作コードを処理するときに、色の値を受け取ります。

ディスプレイドライバーは、次のコードを使用して、ARGB クラス形式と YUV クラス形式の色の値を変換できます。

```cpp
DWORD Convert2N(DWORD Color, DWORD n)
{
    return (Color * (1 << n)) / 256;
}

DWORD CPixel::ConvertFromARGB(D3DCOLOR  InputColor,
                              D3DFORMAT OutputFormat)
{
    DWORD Output = (DWORD) InputColor;
    DWORD Alpha = InputColor >> 24;
    DWORD Red = (InputColor >> 16) & 0x00ff;
    DWORD Green = (InputColor >> 8) & 0x00ff;
    DWORD Blue = InputColor & 0x00ff;
    switch(OutputFormat) {
    case D3DFMT_R8G8B8:
    case D3DFMT_X8R8G8B8:
        Output = InputColor & 0x00ffffff;
        break;

    case D3DFMT_A8R8G8B8:
        Output = InputColor;
        break;

    case D3DFMT_R5G6B5:
        Output = (Convert2N(Red,5) << 11) | 
                    (Convert2N(Green,6) << 5) | 
                    (Convert2N(Blue,5));
        break;

    case D3DFMT_X1R5G5B5:
        Output = (Convert2N(Red,5) << 10) | 
                    (Convert2N(Green,5) << 5) | 
                    (Convert2N(Blue,5));
        break;

    case D3DFMT_A1R5G5B5:
        Output = (Convert2N(Alpha, 1) << 15) | 
                    (Convert2N(Red,5) << 10) | 
                    (Convert2N(Green,5) << 5) | 
                    (Convert2N(Blue,5));
        break;

    case D3DFMT_X4R4G4B4:
        Output = (Convert2N(Red,4) << 8) | 
                    (Convert2N(Green,4) << 4) | 
                    (Convert2N(Blue,4));
        break;

    case D3DFMT_A4R4G4B4:
        Output = (Convert2N(Alpha,4) << 12) |
                    (Convert2N(Red,4) << 8) | 
                    (Convert2N(Green,4) << 4) | 
                    (Convert2N(Blue,4));
        break;

    case D3DFMT_R3G3B2:
        Output = (Convert2N(Red,3) << 5) | 
                    (Convert2N(Green,3) << 2) | 
                    (Convert2N(Blue,2));
        break;

    case D3DFMT_A8R3G3B2:
        Output = (Alpha << 8) |
                    (Convert2N(Red,3) << 5) | 
                    (Convert2N(Green,3) << 2) | 
                    (Convert2N(Blue,2));
        break;

    case D3DFMT_A2B10G10R10:
        Output = (Convert2N(Alpha,2) << 30) |
                    (Convert2N(Red,10)) | 
                    (Convert2N(Green,10) << 10) | 
                    (Convert2N(Blue,10) << 20);
        break;

    case D3DFMT_X8B8G8R8:
        Output = (Convert2N(Red,8)) | 
                    (Convert2N(Green,8) << 8) | 
                    (Convert2N(Blue,8) << 16);
        break;

    case D3DFMT_A8B8G8R8:
        Output = (Alpha << 24) |
                    (Convert2N(Red,8)) | 
                    (Convert2N(Green,8) << 8) | 
                    (Convert2N(Blue,8) << 16);
        break;

#if (DXPIXELVER > 8)
    case D3DFMT_A2R10G10B10:
        Output = (Convert2N(Alpha,2) << 30) |
                    (Convert2N(Red,10) << 20) | 
                    (Convert2N(Green,10) << 10) | 
                    (Convert2N(Blue,10));
        break;
#endif

    case D3DFMT_UYVY:
#if (DXPIXELVER > 8)
    case D3DFMT_R8G8_B8G8:
#endif
        Output = (Red << 24) |
                    (Green << 16) |
                    (Red << 8) |
                    (Blue);
        break;
 
    case D3DFMT_YUY2:
#if (DXPIXELVER > 8)
    case D3DFMT_G8R8_G8B8:
#endif
        Output = (Green << 24) |
                    (Red << 16) |
                    (Blue << 8) |
                    (Red);
        break;

    case MAKEFOURCC('A', 'Y', 'U', 'V'):
    case MAKEFOURCC('N', 'V', '1', '2'):
    case MAKEFOURCC('Y', 'V', '1', '2'):
    case MAKEFOURCC('I', 'C', 'M', '1'):
    case MAKEFOURCC('I', 'C', 'M', '2'):
    case MAKEFOURCC('I', 'C', 'M', '3'):
    case MAKEFOURCC('I', 'C', 'M', '4'):
        Output = InputColor;
        break;
    }
    return Output;
}
```

 

 





