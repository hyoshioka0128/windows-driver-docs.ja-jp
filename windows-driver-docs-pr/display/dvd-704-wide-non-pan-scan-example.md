---
title: DVD 704 全体のパン スキャンではない例
description: DVD 704 全体のパン スキャンではない例
ms.assetid: df335e5e-4f7c-440a-88ef-00f6e0f916e2
keywords:
- アルファ ブレンド組み合わせ WDK DirectX va なので、DVD 704 全体のパン スキャンではない例
- ブレンド画像 WDK DirectX va なので、DVD 704 全体のパン スキャンではない例
- DVD 704 全体パン スキャンではない例 WDK DirectX VA
- 704 全体パン スキャンではない例 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c9e6580ecd28b2eb4aaff7df6a90fa8e3b91d62
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553007"
---
# <a name="dvd-704-wide-non-pan-scan-example"></a>DVD 704 全体のパン スキャンではない例


## <span id="ddk_dvd_704_wide_non_pan_scan_example_gg"></span><span id="DDK_DVD_704_WIDE_NON_PAN_SCAN_EXAMPLE_GG"></span>


704 全体の画像の mpeg-2 DVD での使用をデコード済み画像の境界を超えるソース四角形が必要です (で説明されているメソッドを使用して場合[mpeg-2 パン スキャン例](mpeg-2-pan-scan-example.md))。 この場合は、DVD を指定します、*表示\_水平\_サイズ*を超える、デコードされた画像の 720 の*水平\_サイズ*704 の。 ホスト ソフトウェア デコーダーは割り当てられたソース範囲の外に到達して元の四角形をトリミングを調整する先の四角形を管理するため担当ソース四角形がデコード済み画像の境界を超えた場合トリミングします。

元の四角形がによって定義されている、 **PictureSourceRect16thPel**のメンバー、 [ **DXVA\_BlendCombination** ](https://msdn.microsoft.com/library/windows/hardware/ff563120)構造 (の 16 分の 1 つで、輝度サンプル間隔の解像度) で、次の値。

-   **left** = 0

-   **適切な**= 16 X (**左** + *水平\_サイズ*) 11264 を =

画像のコピー先の四角形がによって定義されている、 **PictureDestinationRect**のメンバー、 [ **DXVA\_BlendCombination** ](https://msdn.microsoft.com/library/windows/hardware/ff563120) (構造体輝度サンプル間隔の解像度の 16 分の 1 つ) を次の 2 つの方法の 1 つ。

1.  次の値で四角形。
    -   **左**= (*表示\_水平\_サイズ*âˆ'*水平\_サイズ*)/2 = 8
    -   **適切な** = **左** + *水平\_サイズ*712 を =

2.  次の値で四角形。
    -   **left** = 0
    -   **適切な** = **左** + *水平\_サイズ*704 を =

2 番目のケースでは、四角形がで示される、 **GraphicDestinationRect**のメンバー、 [ **DXVA\_BlendCombination** ](https://msdn.microsoft.com/library/windows/hardware/ff563120)に構造体がずれている場合、左シフトの画像の保存先を補正する 8 つのサンプルです。

これら 2 つの方法の 2 つ目は、表示に使用するコピー先の領域のみを作成します。

 

 





