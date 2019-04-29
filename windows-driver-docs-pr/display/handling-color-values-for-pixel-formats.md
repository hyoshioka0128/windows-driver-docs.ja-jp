---
title: ピクセル形式の色の値の処理
description: ピクセル形式の色の値の処理
ms.assetid: 53ce6be1-14e1-4ee8-ba29-f198dcdacdaa
keywords:
- WDK DirectX 9.0 のピクセル形式の色の値
- WDK DirectX 9.0 のピクセル形式のカラー値します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ddd4a844e8a7edcdd159d0425b5ae0e5300ebda3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323720"
---
# <a name="handling-color-values-for-pixel-formats"></a>ピクセル形式の色の値の処理


## <span id="ddk_handling_color_values_for_pixel_formats_gg"></span><span id="DDK_HANDLING_COLOR_VALUES_FOR_PIXEL_FORMATS_GG"></span>


**このトピックには、DirectX 7.0 以降が適用されます。**

アプリケーションが一貫した方法で塗りつぶしの色とこれらの形式とサーフェスでクリア操作を要求できるため、ディスプレイ ドライバーは色形式の ARGB と YUV クラスの入力色の値を変換する必要があります。 ただし、ドライバーは、他のクラスの形式の色の値を直接使用する必要があります。 たとえば、アプリケーション A8R8G8B8、均一な色の値として使用を最大で 8 ビットのアルファ (A)、赤 (R)、緑 (G)、および青 (B) コンポーネントを持つすべての画面ドライバーは、最高の有意性をビットをコピーすることで、実際の ARGB 形式に固有の色の値に A8R8G8B8 色を変換する必要があります。

ディスプレイ ドライバーが、D3DDP2OP を処理するときに、色の値を受け取る\_CLEAR および D3DDP2OP\_COLORFILL 操作のコードでその[ **D3dDrawPrimitives2** ](https://msdn.microsoft.com/library/windows/hardware/ff544704)関数。

ディスプレイ ドライバーは、ARGB と YUV クラス形式の色の値に変換するのに次のコードを使用できます。

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

 

 





