---
title: 低レベルの IDCT 処理要素
description: 低レベルの IDCT 処理要素
ms.assetid: 7736a226-1122-4380-b09f-a8560c0cd609
keywords:
- マクロが WDK DirectX VA、IDCT をブロックする
- 低レベルの IDCT WDK DirectX VA
- オフホスト IDCT WDK DirectX VA
- ホストベースの IDCT WDK DirectX VA
- 逆余弦変換-WDK DirectX VA
- IDCT WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e658c589fcfeb53e0f2cfef3f1ae38de88c40fd1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840594"
---
# <a name="low-level-idct-processing-elements"></a>低レベルの IDCT 処理要素


## <span id="ddk_low_level_idct_processing_elements_gg"></span><span id="DDK_LOW_LEVEL_IDCT_PROCESSING_ELEMENTS_GG"></span>


DirectX VA インターフェイスは、低レベルの逆余弦変換 (*Idct*) を処理するさまざまな方法をサポートしています。 操作には、次の2つの基本的な種類があります。

1.  オフホスト IDCT: 外部 IDCT、画像の再構築、再構築のクリッピングのために、変換係数のマクロブロックをアクセラレータに渡します。

2.  ホストベースの IDCT: ホスト上で IDCT を実行し、空間ドメインの結果のブロックを、外部の画像の再構築と再構築のためのアクセラレータに渡します。

どちらの場合も、基本的な逆量子化プロセス、IDCT 範囲の鮮やかさ、MPEG-2 不一致の制御 (必要な場合)、および DC 内のオフセット (必要な場合) がホストで実行されます。 どちらの場合も、最終的な画像の再構築と再構築のクリッピングは、アクセラレータで行われます。

逆量子化、IDCT の前の鮮やかさ、不一致の制御、DC 間のオフセット、IDCT、画像の再構築、および再構築のクリッピングプロセスは、次の手順で定義されています。 [**DXVA\_QmatrixData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_qmatrixdata)構造体は、圧縮されたビデオ画像デコード用の逆量子化行列データを読み込みます。 ( [**DXVA\_ピクチャパラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)構造体で特に指定されていない限り、 *BPP*、 *W*<sub>t</sub>、および*H*<sub>t</sub>の値は8と同じである必要があります)。

1. 必要に応じて (逆量子重み付け行列の適用を含む) 逆量子化を実行して、エントロピでコード化された量子化インデックスから IDCT 係数値*F "(u, v)* のセットを作成します。 これはホストによって実行されます。

2. 変換係数ブロックの再構築された各係数値*f "(u, v)* を飽和状態にして、次の式で定義されている制限付き許容範囲内の値*f ' (u, v)* を取得します。 これはホストによって実行されます。前に逆余弦変換 (idct) の彩度を示す![計算](images/formula1.png)

3. MPEG-2 の不一致コントロールを実行します。 (この処理の段階は、MPEG 2 でのみ必要です)。一致しないコントロールは、マクロブロック内のすべての係数の飽和値を合計することによって実行されます (これは、最下位ビットを隠ぺいするすることと同じです)。 合計が偶数の場合、1は最後の係数*F '* (*W*<sub>t</sub> *-1, H*<sub>t</sub> *-1*) の飽和値から減算されます。 合計が奇数の場合、 *F ' (W*<sub>t</sub> *-1, H*<sub></sub><em>-1)</em>*の飽和値は、変更されずにそのまま<strong><em>使用されます。このドキュメントでは、鮮やかさと不一致の制御の後に作成される係数値を * F (u, v) と呼び</em>ます。これはホストによって実行されます。* * メモ</strong>MPEG-1 には、逆量子化後に偶数の値を持つ係数ごとにプラスまたはマイナス1で値を変更することで構成される不一致コントロールのさまざまな形式があります。 このセクションで説明する不一致コントロールは、263には必要ありません。 いずれの場合も、不一致コントロールは、必要に応じてホストの役割です。

     

4. 必要に応じて、すべてのブロックに DC 間オフセットを追加します。これにより、すべてのブロックは、空間参照の予測値 2<sup>(BPP-1)</sup>に対する相対的な差を表します。 このようなオフセットは、参照されているすべてのビデオコーディング標準 (DXVA、MPEG-2、MPEG-4) で必要です。ただし、 *Hostresiddiff*が1で、の**Bconfig\_** のメンバーが[**configピクチャデコードである場合を除きます。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode)構造は1です。 DC 内のオフセットには、変換ドメインの値 (2<sup>(BPP-1)</sup>) \* Sqrt (*W*<sub>t</sub>*H*<sub>t</sub>) があります。 この値は、 *BPP*を8より大きくすることを許可する mpeg-2 以外のすべての場合に1024です。 これはホストによって実行されます。

5. ホストまたはアクセラレータで逆離散余弦変換 (IDCT) を実行します。 Idct は、次の式で指定されます。ここでは、 *c*(*u*) = 1 ( *u* = 0)、それ以外の場合は*c (u)* = sqrt (2) *c*(*v*) = 1、 *v* = 0、それ以外の場合、 *c (v)* = sqrt (2) *x*と*y*が横ピクセルドメイン*u*および*v*の垂直方向の空間座標は、変換ドメインの水平方向と垂直方向の周波数座標です。 *W*<sub>t</sub>と*H*<sub>t</sub>は変換ブロックの幅と高さです。(通常、両方とも 8)。
6. 空間ドメインの残差情報を、非内部ブロックの[モーション補正予測](motion-compensated-prediction.md)値に追加するか、ブロック内の定数参照値に追加して、アクセラレータでの画像の再構築を実行します。 内部ブロックの定数参照値は 2<sup>(BPP-1) です。</sup>ただし、HostResidDiff (DXVA の**wmbtype**メンバーのビット 10 [ **\_Mbctrl\_P\_hostresiddiff\_1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_mbctrl_p_hostresiddiff_1)) 構造体は1で、 [**DXVA\_Configピクチャデコード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode)構造体の bconfig メンバーは1です。 後者の場合、定数は0になります。

7. 画像の再構築を 0 ~ (2<sup>BPP</sup>)-1 の範囲にクリップし、最終的に結果として得られる picture サンプル値をアクセラレータに格納します。

 

 





