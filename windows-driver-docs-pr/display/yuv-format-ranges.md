---
title: Windows 8.1 で YUV 形式の範囲
ms.assetid: D76FFB8C-CA42-446E-826F-52982B1849E5
description: ユーザー モードのディスプレイ ドライバーが YUV ビデオ形式の利点を取得する方法
keywords:
- 全範囲 YUV WDK の表示
- 拡張範囲 YUV WDK の表示
- studio 輝度範囲 YUV WDK の表示
- YUV 形式と WMF WDK の表示をサポートします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9343525733da15824bc51ac382e43ff4c0272f5a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372026"
---
# <a name="yuv-format-ranges-in-windows81"></a>Windows 8.1 で YUV 形式の範囲


アプリをユーザー モードのディスプレイ ドライバー拡張範囲を活用するためにシグナル\[0, 255\] YUV ビデオ形式をこの表に示すように、Windows 8.1 で開始します。

| YUV 範囲                | 入力データの範囲 | 一般的な使い方                                           | Standard                                                  |
|--------------------------|------------------|---------------------------------------------------------|-----------------------------------------------------------|
| *拡張範囲*         | \[0, 255\]       | コンシューマーの機器: web カメラとオート フォーカス カメラ | 既定ではビデオ形式を標準、JFIF、MJPEG |
| *studio 輝度の範囲* | \[16, 235\]      | プロフェッショナルなカメラおよびビデオ機器                | ITU BT.601 と BT.709                                     |

 

コンテンツおよびブロードキャスト業界によって生成されたほとんどのビデオは、拡張範囲が個々 のコンシューマーによって生成されたビデオの間に、studio の範囲内でです。 拡張範囲ともいいます*輝度の範囲を完全な*します。

Windows 8.1、Microsoft メディア ファンデーションがビデオ処理パイプラインは、studio の範囲を使用した場合、すべての入力データを処理する前にその結果、ダイナミック レンジの削減と多くの場合、過酷なコントラスト拡張範囲で入力データが実際にされた場合は。

以降、Windows 8.1 のでは入力ビデオの YUV 形式が拡張の範囲内にあるときに、アプリは、この上の動的範囲のドライバーに通知できます。

## <a name="span-idconvertingextended-rangeyuvformatspanspan-idconvertingextended-rangeyuvformatspanspan-idconvertingextended-rangeyuvformatspanconverting-extended-range-yuv-format"></a><span id="Converting_extended-range_YUV_format"></span><span id="converting_extended-range_yuv_format"></span><span id="CONVERTING_EXTENDED-RANGE_YUV_FORMAT"></span>拡張範囲 YUV 形式に変換します。


これらのイメージから暗い光の値の範囲 YUV 拡張範囲のコンテンツを変換する方法 (解釈) に表示形式の RGB:

-   一番上のイメージは、studio の範囲の場合と同様に、解釈を正しく拡張範囲コンテンツを示します。
-   下側のイメージでは、正しく解釈拡張範囲のコンテンツを示します。

一番上のイメージが正しく解釈されないはコントラストを示し、純粋な白に達する前に過度に明るくなり強調表示になります。

![拡張範囲 yuv コンテンツの正しくないと正しく解釈の比較](images/extended-range-yuv.png)

## <a name="span-idextended-rangeyuvinterfacespanspan-idextended-rangeyuvinterfacespanspan-idextended-rangeyuvinterfacespanextended-range-yuv-interface"></a><span id="Extended-range_YUV_interface"></span><span id="extended-range_yuv_interface"></span><span id="EXTENDED-RANGE_YUV_INTERFACE"></span>拡張範囲 YUV インターフェイス


Windows 8.1、メディア ファンデーション studio 輝度の範囲にサポートされるのみ、前にため拡張範囲のイメージの解釈が発生した増加とは異なり、上記の最初の図のようにします。 メディア ファンデーション パイプラインは、使用してこれらの構造体を Windows 8.1 以降、および拡張範囲かどうかを Windows 表示 Driver Model (WDDM) 1.3 およびそれ以降のユーザー モードを示す列挙体がドライバーを表示または studio 範囲 YUV コンテンツが再生中またはキャプチャされます。

### <a name="span-idnewenumerationsspanspan-idnewenumerationsspanspan-idnewenumerationsspannew-enumerations"></a><span id="New_enumerations"></span><span id="new_enumerations"></span><span id="NEW_ENUMERATIONS"></span>新しい列挙体

-   [**D3D11\_1DDI\_ビデオ\_プロセッサ\_公称\_範囲**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ne-d3d10umddi-d3d11_1ddi_video_processor_nominal_range)
-   [**DXVAHDDDI\_公称\_範囲**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ne-d3dumddi-_dxvahdddi_nominal_range)

### <a name="span-idchangedstructuresandenumerationsspanspan-idchangedstructuresandenumerationsspanspan-idchangedstructuresandenumerationsspanchanged-structures-and-enumerations"></a><span id="Changed_structures_and_enumerations"></span><span id="changed_structures_and_enumerations"></span><span id="CHANGED_STRUCTURES_AND_ENUMERATIONS"></span>変更された構造および列挙体

-   [**D3D11\_1DDI\_ビデオ\_プロセッサ\_色\_領域**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d11_1ddi_video_processor_color_space)
-   [**D3D11\_1DDI\_ビデオ\_プロセッサ\_デバイス\_キャップ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ne-d3d10umddi-d3d11_1ddi_video_processor_device_caps)
-   [**DXVAHDDDI\_BLT\_STATE\_OUTPUT\_COLOR\_SPACE\_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_dxvahdddi_blt_state_output_color_space_data)
-   [**DXVAHDDDI\_STREAM\_STATE\_INPUT\_COLOR\_SPACE\_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_dxvahdddi_stream_state_input_color_space_data)
-   [**DXVAHDDDI\_VPDEVCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_dxvahdddi_vpdevcaps)

**注**  WDDM 1.3、および大きいユーザー モードのディスプレイ ドライバーはこれらの追加または変更された構造および列挙体のすべてでサポートする必要があります。

 

参照してください[YUV RGB データ変換の範囲は](yuv-rgb-data-range-conversions.md)異なる入力 RGB と YUV 間で変換する方法の詳細について、書式設定します。

 

 





