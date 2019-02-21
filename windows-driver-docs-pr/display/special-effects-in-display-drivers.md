---
title: ディスプレイ ドライバーでの特殊効果
description: ディスプレイ ドライバーでの特殊効果
ms.assetid: f44a89df-6412-442c-8491-3e2f2bbd826f
keywords:
- ディスプレイ ドライバー WDK Windows 2000 では、特殊効果
- Windows 2000 の WDK の特殊効果を表示します。
- Windows 2000 の WDK の効果を表示します。
- blend でアニメーション WDK Windows 2000 を表示します。
- blend アウト アニメーション WDK Windows 2000 を表示します。
- Windows 2000 の WDK アルファのカーソルを表示します。
- グラデーション塗りつぶし WDK Windows 2000 を表示します。
- アルファ ブレンディング WDK Windows 2000 の表示
- ビット ブロック転送 WDK Windows 2000 の表示
- Windows 2000 の WDK の表示を拡大
- Windows 2000 の WDK のアニメーションを表示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3390248bdfc81aba6604f2abe79d7cd395d99bfb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536144"
---
# <a name="special-effects-in-display-drivers"></a>ディスプレイ ドライバーでの特殊効果


## <span id="ddk_special_effects_in_display_drivers_gg"></span><span id="DDK_SPECIAL_EFFECTS_IN_DISPLAY_DRIVERS_GG"></span>


Windows 2000 と以降のオペレーティング システム バージョンは、次の特殊効果をサポートします。

-   ディスプレイ ハードウェアでは、アルファ ブレンドをサポートする場合、ディスプレイ ドライバーを実装できます[ **DrvAlphaBlend**](https://msdn.microsoft.com/library/windows/hardware/ff556176)します。

-   ディスプレイ ハードウェアでは、グラデーション塗りつぶしをサポートする場合、ディスプレイ ドライバーを実装する必要があります[ **DrvGradientFill**](https://msdn.microsoft.com/library/windows/hardware/ff556236)します。

### <a name="span-idalphablendingspanspan-idalphablendingspanspan-idalphablendingspanalpha-blending"></a><span id="Alpha_Blending"></span><span id="alpha_blending"></span><span id="ALPHA_BLENDING"></span>アルファ ブレンド

Microsoft Windows 2000 (以降) シェルを使用してアルファ ブレンド広くなどの操作を実行する*blend で*と*blend アウト アニメーション*と*アルファ カーソル*します。 アルファ ブレンド操作には、ソースと宛先の両方のサーフェスからの読み取りが必要とするため、元または送信先のいずれかがビデオ メモリの場合は、GDI を後回しに非常に低速です。 その結果、ドライバーのハードウェア アクセラレーションは視覚的により滑らかなアニメーションを生成し、全体的なシステム パフォーマンスが向上します。

ドライバーを実装する必要があります**DrvAlphaBlend**、その継ぎ目がこれまで表示されません。

によって生成される最悪の場合、エラー *DrvAlphaBlend*ごとに 1 つ (1) のカラー チャネルを超えない必要があります。 ソースがブレンド; より前に、Windows SDK のドキュメントを COLORONCOLOR 拡大 (参照) をする必要があります拡大が関係する場合最悪の場合、エラーが超えないようにごとに 1 つ (1)、最悪の伸縮エラーと組み合わせてカラー チャネル。

Wdk のディスプレイ ドライバーの実装を評価するテストがある場所、拡大を使用した結合はアルファ ブレンドの場合、 *DrvAlphaBlend*次のようにします。

1.  テストの呼び出し、ディスプレイ ドライバーの*DrvAlphaBlend*、アルファ ブレンドと拡張の四角形を生成します。

2.  テストへの呼び出しで使用されていた同じソース四角形を使用して、移行先四角形を生成する*DrvAlphaBlend*します。

3.  各ピクセルの P 手順 2. の先の四角形で、テストは、拡大する前に元の四角形内の対応するピクセルを決定する逆引き stretch をシミュレートします。 テストでは、ドライバーによって、さまざまな拡張の実装を対応するために逆方向の拡張を行うの許容範囲値が適用されます。 テストは、そのピクセルに適用する必要がありますアルファ ブレンドを計算します。

    ため、4 つの可能なピクセル (角の 3 x 3 ピクセルの正方形のピクセル P の中央に配置) のいずれかのソースの四角形を拡大でした先の四角形のピクセル P を生成するために、テストが番目のピクセルのコーナーの各ピクセルの色の値を比較する必要がありますによって生成された四角形内の対応する位置の e *DrvAlphaBlend*します。

最悪の伸縮エラーは、色の値のペアのうち 1 つが対応する上隅にあるピクセルの間の最大差、 *DrvAlphaBlend*の四角形を生成し、もう一方のテストで生成されたソース四角形。

### <a name="span-idgradientfillsspanspan-idgradientfillsspanspan-idgradientfillsspangradient-fills"></a><span id="Gradient_Fills"></span><span id="gradient_fills"></span><span id="GRADIENT_FILLS"></span>グラデーションの塗りつぶし

Windows 2000 (以降) のシェルを使用して*グラデーション塗りつぶし*すべてのキャプション バー。

によって生成される結果[ **DrvGradientFill** ](https://msdn.microsoft.com/library/windows/hardware/ff556236) 、ピクセルあたりのビット数に依存し、次のガイドラインを満たす必要があります。

### <a name="span-id24bppor32bppsurfacesspanspan-id24bppor32bppsurfacesspan24-bpp-or-32-bpp-surfaces"></a><span id="_24_bpp_or_32_bpp_surfaces"></span><span id="_24_BPP_OR_32_BPP_SURFACES"></span>24 bpp、または 32 bpp のサーフェス

-   値必要がありますを増減させる単調 gradated 全方向にします。

-   グラデーションの四角形。ときに*ulMode*グラデーションを = =\_入力\_RECT\_H、各縦棒は、1 つの色である必要があります。
    ときに*ulMode*グラデーションを = =\_入力\_RECT\_V、各横棒は 1 つの色である必要があります。
-   任意のチャンネルにおける最悪の場合、エラーは、Â±1 を超えることはできません。

-   リージョンのエンドポイントは、完全一致である必要があります。

### <a name="span-id15bppor16bppsurfacesspanspan-id15bppor16bppsurfacesspan15-bpp-or-16-bpp-surfaces"></a><span id="_15_bpp_or_16_bpp_surfaces"></span><span id="_15_BPP_OR_16_BPP_SURFACES"></span>bpp 15 または 16 bpp のサーフェス

任意のチャンネルにおける最悪の場合、エラーは、Â±15 を超えることはできません。

### <a name="span-id1bppto8bppsurfacesspanspan-id1bppto8bppsurfacesspan1-bpp-to-8-bpp-surfaces"></a><span id="_1_bpp_to_8_bpp_surfaces"></span><span id="_1_BPP_TO_8_BPP_SURFACES"></span>8-ビット/ピクセルの表面に 1 のビット/ピクセル

これらのサーフェスのいずれかのグラデーションの塗りつぶしにエラーが許可されていません。 8 bpp サーフェス、GDI 呼び出しませんドライバーの*DrvGradientFill*関数。

すべてのサーフェスでクリッピング影響を及ぼさないように結果に注意してください。

 

 





