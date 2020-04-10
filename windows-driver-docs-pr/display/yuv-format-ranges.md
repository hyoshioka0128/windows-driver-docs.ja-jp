---
title: Windows 8.1 の YUV 形式の範囲
ms.assetid: D76FFB8C-CA42-446E-826F-52982B1849E5
description: ユーザーモード表示ドライバーが YUV ビデオ形式を利用する方法
keywords:
- 全範囲の YUV WDK 表示
- 拡張範囲の YUV WDK ディスプレイ
- studio 輝度範囲の YUV WDK ディスプレイ
- YUV 形式と WMF サポート WDK ディスプレイ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8cace8c30123178e15027200daf0729cd3c2bd3
ms.sourcegitcommit: 329eee396e727bbd1b2a096a5c7bb0c4b78f52e5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/10/2020
ms.locfileid: "81007814"
---
# <a name="yuv-format-ranges-in-windows81"></a>Windows 8.1 の YUV 形式の範囲


アプリでは、次の表に示すように、Windows 8.1 で始まる範囲の \[0、255\] YUV ビデオ形式を利用するようにユーザーモードのディスプレイドライバーに通知できます。

| YUV 範囲                | 入力データ範囲 | 一般的な使い方                                           | 標準                                                  |
|--------------------------|------------------|---------------------------------------------------------|-----------------------------------------------------------|
| *拡張範囲*         | \[0、255\]       | コンシューマー機器: webcam とポイントアンドシューティングカメラ | JFIF standard および MJPEG ビデオ形式が既定値として使用される |
| *studio の輝度範囲* | \[16、235\]      | プロのカメラとビデオ機器                | ITU BT および BT. 709                                     |

 

コンテンツおよび放送業界によって生成されるほとんどのビデオは studio の範囲内であり、個々のコンシューマーによって生成されるビデオは拡張範囲に含まれています。 拡張範囲は、*完全な輝度の範囲*とも呼ばれます。

Windows 8.1 前に、Microsoft メディアファンデーションビデオ処理パイプラインは、すべての入力データを studio の範囲内にあるかのように処理します。これにより、動的な範囲が縮小され、入力データが実際には拡張範囲内にある場合には、多くの場合、強いコントラストが得られます。

Windows 8.1 以降では、ビデオ入力の YUV 形式が拡張範囲内にある場合、アプリはこの高いダイナミックレンジのドライバーに通知できます。

## <a name="span-idconverting_extended-range_yuv_formatspanspan-idconverting_extended-range_yuv_formatspanspan-idconverting_extended-range_yuv_formatspanconverting-extended-range-yuv-format"></a><span id="Converting_extended-range_YUV_format"></span><span id="converting_extended-range_yuv_format"></span><span id="CONVERTING_EXTENDED-RANGE_YUV_FORMAT"></span>拡張範囲の YUV 形式の変換


これらのイメージは、dark から明るい値までの範囲の YUV 拡張範囲コンテンツを RGB 形式に変換する方法を示しています。

-   上部の画像は、拡張範囲のコンテンツが studio の範囲であるかのように誤って解釈されることを示しています。
-   下の画像は、拡張範囲のコンテンツが正しく解釈されていることを示しています。

上の図の不適切な解釈により、コントラストが大きくなり、純粋な白に達する前に強調表示が非常に明るくなります。

![拡張範囲の yuv コンテンツの正しくない解釈と正しい解釈の比較](images/extended-range-yuv.png)

## <a name="span-idextended-range_yuv_interfacespanspan-idextended-range_yuv_interfacespanspan-idextended-range_yuv_interfacespanextended-range-yuv-interface"></a><span id="Extended-range_YUV_interface"></span><span id="extended-range_yuv_interface"></span><span id="EXTENDED-RANGE_YUV_INTERFACE"></span>拡張範囲の YUV インターフェイス


Windows 8.1 する前に、サポートされている studio の輝度範囲だけをメディアファンデーションします。そのため、上の最初の図に示すように、拡張範囲のイメージを解釈すると、コントラストが向上しました。 Windows 8.1 以降、メディアファンデーションパイプラインは、これらの構造と列挙を使用して、拡張範囲または studio 範囲の YUV コンテンツが再生またはキャプチャされているかどうかを Windows Display Driver Model (WDDM) 1.3 以降のユーザーモード表示ドライバーに示します。

### <a name="span-idnew_enumerationsspanspan-idnew_enumerationsspanspan-idnew_enumerationsspannew-enumerations"></a><span id="New_enumerations"></span><span id="new_enumerations"></span><span id="NEW_ENUMERATIONS"></span>新しい列挙型

-   [**D3D11\_1DDI\_ビデオ\_プロセッサ\_公称\_範囲**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1ddi_video_processor_nominal_range)
-   [**DXVAHDDDI\_公称\_範囲**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-_dxvahdddi_nominal_range)

### <a name="span-idchanged_structures_and_enumerationsspanspan-idchanged_structures_and_enumerationsspanspan-idchanged_structures_and_enumerationsspanchanged-structures-and-enumerations"></a><span id="Changed_structures_and_enumerations"></span><span id="changed_structures_and_enumerations"></span><span id="CHANGED_STRUCTURES_AND_ENUMERATIONS"></span>変更された構造体と列挙型

-   [**D3D11\_1DDI\_ビデオ\_プロセッサ\_色\_領域**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddi_video_processor_color_space)
-   [**D3D11\_1DDI\_ビデオ\_プロセッサ\_デバイス\_キャップ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1ddi_video_processor_device_caps)
-   [**DXVAHDDDI\_BLT\_状態\_出力\_色\_領域\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvahdddi_blt_state_output_color_space_data)
-   [**DXVAHDDDI\_STREAM\_状態\_入力\_色\_領域\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvahdddi_stream_state_input_color_space_data)
-   [**DXVAHDDDI\_VPDEVCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvahdddi_vpdevcaps)

**注**  WDDM 1.3 以降のユーザーモード表示ドライバーでは、これらの新規および変更された構造と列挙型のすべてをサポートする必要があります。

 

異なる入力 RGB 形式と YUV 形式間で変換する方法の詳細については、「 [YUV-rgb データ範囲変換](yuv-rgb-data-range-conversions.md)」を参照してください。

 

 





