---
title: 8 ビット YUV の色空間の処理
description: 8 ビット YUV の色空間の処理
ms.assetid: fbf62dc6-b5bf-43f6-baa8-c6d1cee80f9b
keywords:
- ProcAmp WDK DirectX VA、YUV 色空間
- YUV 形式 WDK DirectX VA
- Y 処理 WDK DirectX VA
- UV 処理 WDK DirectX VA
- 色空間の変換が WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b6b1094784003e6541d6569759c32f9c05ff419
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559471"
---
# <a name="processing-in-the-8-bit-yuv-color-space"></a>8 ビット YUV の色空間の処理


## <span id="ddk_processing_in_the_8_bit_yuv_color_space_gg"></span><span id="DDK_PROCESSING_IN_THE_8_BIT_YUV_COLOR_SPACE_GG"></span>


YUV の色空間での作業には、ビデオ ストリームの ProcAmp 調整コントロールの関連する計算が簡略化します。

### <a name="span-idyprocessingspanspan-idyprocessingspanspan-idyprocessingspany-processing"></a><span id="Y_Processing"></span><span id="y_processing"></span><span id="Y_PROCESSING"></span>Y の処理

ProcAmp 調整の Y コンポーネントを実行するには、16 0 では、黒のレベルを配置する Y 値を減算します。 これにより、コントラストを調整することも、黒のレベルは変化しないように、DC のオフセットを削除します。 Y 値には、16 より小さい可能性があります、ため、負の値の Y 値がこの時点でサポートされている必要があります。 コントラストを調整するには、定数 YUV ピクセル値を乗算します。 U および V は調整されません、色ずれはコントラストが変更されるたびに発生します。 明るさプロパティの値が追加 (または減算) からコントラストの調整の Y 値。これは、コントラストを調整するための DC のオフセットを導入しないようにします。 最後に、値 16 は、16 では、黒のレベルを再配置に追加されます。

次の式では、前の段落で説明されている手順をまとめたものです。 C はコントラスト値で、B は、明るさの値です。

```cpp
Y&#39; = ((Y - 16) x C) + B + 16
```

### <a name="span-iduvprocessingspanspan-iduvprocessingspanspan-iduvprocessingspanuv-processing"></a><span id="UV_Processing"></span><span id="uv_processing"></span><span id="UV_PROCESSING"></span>UV の処理

ProcAmp の調整を実行するおよび V のコンポーネントが、両方 V の値を約 0 の範囲を配置から 128 を減算します。 Hue プロパティを組み合わせることで実装され、次の数式で示すように V の値します。 目的の色合い角度、H は。

```cpp
U&#39; = (U-128) x Cos(H) + (V-128) x Sin(H)
V&#39; = (V-128) x Cos(H) - (U-128) x Sin(H)
```

彩度が U を乗算して調整 'v' を組の定数、しに 128 を追加しています。 次の数式では、色相と彩度 UV データでの結合の処理が表示されます。 目的の色合い角度、H は、C は、コントラスト値および S が鮮やかさの値。

```cpp
U&#39;&#39; = (((U-128) x Cos(H) + (V-128) x Sin(H)) x C x S) + 128
V&#39;&#39; = (((V-128) x Cos(H) - (U-128) x Sin(H)) x C x S) + 128
```

 

 





