---
title: MPEG-2 パン スキャンの例
description: MPEG-2 パン スキャンの例
ms.assetid: 6ce4722c-5406-4b29-9171-ecab049320e7
keywords:
- アルファ ブレンドの組み合わせ WDK DirectX va なので、mpeg-2 パン スキャンの使用例
- ブレンド mpeg-2 画像 WDK DirectX va なので、パン スキャンの使用例
- PictureSourceRect16thPel
- Mpeg-2 パン スキャン WDK DirectX VA の使用例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a367dbac7ed5f8a20060b8e26068157d703e12b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353018"
---
# <a name="mpeg-2-pan-scan-example"></a>MPEG-2 パン スキャンの例


## <span id="ddk_mpeg_2_pan_scan_example_gg"></span><span id="DDK_MPEG_2_PAN_SCAN_EXAMPLE_GG"></span>


ときに、 **PictureSourceRect16thPel**のメンバー、 [ **DXVA\_BlendCombination** ](https://msdn.microsoft.com/library/windows/hardware/ff563120)構造を使用して、mpeg-2 ビデオのパン スキャンで指定された領域を選択しますパラメーターの値は、 **PictureSourceRect16thPel**メンバーは、次の式を使用して計算することができます。 これらの値にする必要がありますを使用する場合は、アルファ ブレンドの組み合わせのバッファーの記載された制限に違反していない**PictureSourceRect16thPel**します。 詳細については、次を参照してください。、**解説**は、DXVA セクション\_BlendCombination 構造体。

Mpeg-2 パン スキャン パラメーターとパラメーターを具体的には、いくつかの調整を必要とする、いくつかの mpeg-2 dvd の収録内容でこれらの制約に違反する可能性があります、 **PictureSourceRect16thPel**します。

-   **左**= 8 x (*水平\_サイズ* - *表示\_水平\_サイズ*)-*フレーム\_centre\_水平\_オフセット*

-   **上部**= 8 x (*垂直\_サイズ - 表示\_垂直\_サイズ*)-*フレーム\_centre\_垂直\_オフセット*

-   **適切な** = **左**+ (16 x*表示\_水平\_サイズ*)

-   **下部にある** = **上部**+ (16 x*表示\_垂直\_サイズ*)

**PictureDestinationRect**メンバーは、DXVA の\_BlendCombination 構造は通常は、次の値を使用し。

-   **左**= 0 または 8 (うに[DVD 704 全体の非-パンの例の画像をスキャン](dvd-704-wide-non-pan-scan-example.md))

-   **上部**= 0

-   **適切な** = **左** + *表示\_水平\_サイズ*

-   **下部にある** = **上部** + *表示\_垂直\_サイズ*

 

 





