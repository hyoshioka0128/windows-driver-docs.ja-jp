---
title: 低レベルの IDCT 処理要素
description: 低レベルの IDCT 処理要素
ms.assetid: 7736a226-1122-4380-b09f-a8560c0cd609
keywords:
- マクロ ブロック WDK DirectX va なので、IDCT
- 低レベルの IDCT WDK DirectX VA
- オフホスト IDCT WDK DirectX VA
- ホスト ベース IDCT WDK DirectX VA
- 逆コサイン不連続変換 WDK DirectX VA
- IDCT WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03e8d30d07de56ac537e0e7a28f1fc2786b5c655
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537205"
---
# <a name="low-level-idct-processing-elements"></a>低レベルの IDCT 処理要素


## <span id="ddk_low_level_idct_processing_elements_gg"></span><span id="DDK_LOW_LEVEL_IDCT_PROCESSING_ELEMENTS_GG"></span>


DirectX VA インターフェイスには、低レベルの逆コサイン不連続変換処理のさまざまな方法がサポートされています (*IDCT*)。 2 つの基本的な種類の操作があります。

1.  オフホスト IDCT:アクセラレータに外部 IDCT、画像の再構築、および再構築のクリッピングの変換係数のマクロ ブロックを渡します。

2.  ホスト ベース IDCT:外部の画像の再構築および再構築のクリッピング アクセラレータにドメイン空間結果のホストを渡してブロックに、IDCT を実行します。

どちらの場合も、逆量子化の基本的なプロセス、プレ IDCT 範囲彩度、mpeg-2 不一致コントロール (必要に応じて)、および内通信 DC のオフセット (必要な) 場合は、ホストで実行されます。 どちらの場合も、最終的な画像の再構築と再構築のクリッピングが、アクセラレータ上で実行されます。

逆の量子化、プレ IDCT 彩度、不一致コントロール、内通信 DC オフセット、IDCT、画像の再構築、およびクリッピングのプロセスを再構築は、次の手順で定義されます。 [ **DXVA\_QmatrixData** ](https://msdn.microsoft.com/library/windows/hardware/ff564034)構造が圧縮ビデオ画像のデコード、逆量子化のマトリックスのデータを読み込みます。 (値の*BPP*、 *W*<sub>T</sub>、および*H*<sub>T</sub> 8 に等しいことを前提としない限り、それ以外の場合指定された、 [ **DXVA\_PictureParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff564012)構造です)。

1. IDCT 係数の値のセットを作成するときに逆の量子化 (逆量子化の重み付けのマトリックスのアプリケーション) を含む、必要に応じて*F"(u,v)* 量子化のエントロピ-コード化されたインデックスから。 これは、ホストで実行されます。

2. 再構築された係数値ごとの飽和*F"(u,v)* の値を取得する変換係数ブロック*F'(u,v)* 次の数式で定義された制限付きの有効な範囲内です。 これは、ホストで実行されます。![事前逆の不連続のコサインを表す計算 (事前 idct) の鮮やかさを変換します。](images/formula1.png)

3. Mpeg-2 の不一致の制御を実行します。 (この段階の処理は必要 mpeg-2 のみ。)不一致のコントロールは、マクロ ブロック内のすべての係数の飽和させられた値を合計によって実行されます (xor を実行するのと同じ、最下位ビット)。 最後の係数の飽和させられた値から 1 を減算する合計が偶数の場合*F'*(*W*<sub>T</sub>*-1、H*<sub>T</sub>*-1*)。 合計が、奇数の場合の飽和させられた値*F'(W*<sub>T</sub>*-1、H*<sub>T</sub><em>-1)</em> * <strong><em>は、変更せずに使用されます。係数値の彩度 との不一致のコントロールの後に作成される *F(u,v) と呼びます</em>このドキュメントで。これは、ホストで実行されます。* * 注</strong>mpeg-1 プラスまたはマイナス 1 を逆の量子化した後でも、値を持つそれ以外の場合はそれぞれの係数の値を変更することで構成される不一致コントロールのさまざまな形式があります。 H.263 では、このセクションで説明されている不一致コントロールは必要ありません。 いずれの場合も、不一致のコントロールは必要な場合は、ホストの責任です。

     

4. ブロックを追加します (必要に応じて) のオフセット内の DC 内のすべてを内のすべてのブロックが 2 の空間参照予測値を基準に、差を表すように<sup>(BPP 1)</sup>します。 このようなオフセットはすべて、参照されたビデオ コーディング標準 (H.261、H.263、mpeg-1、mpeg-2 および mpeg-4) 場合を除きために必要な*HostResidDiff* 1 は、および**bConfigIntraResidUnsigned**のメンバー、[ **DXVA\_ConfigPictureDecode** ](https://msdn.microsoft.com/library/windows/hardware/ff563133)構造体は 1 です。 内の DC のオフセットが、値 (2<sup>(BPP 1)</sup>) \* sqrt (*W*<sub>T</sub>*H*<sub>T</sub>) で、ドメインを変換します。 この値は、mpeg-4 を除くすべてのケースで 1024 *BPP* 8 より大きくなります。 これは、ホストで実行されます。

5. ホストまたはアクセラレータでは、個別の逆コサイン変換 (IDCT) を実行します。 次の数式によって、IDCT が指定された場所。*C*(*u*) = 1 を*u*それ以外の場合、0 を = *C(u)* = sqrt(2) *C*(*v*)の1を=*v*それ以外の場合、0 を = *C(v)* = sqrt(2) *x*と*y*ピクセル ドメインで水平方向および垂直方向の空間座標*u*と*v*変換ドメインの頻度を水平および垂直座標*W*<sub>T</sub>と*H*<sub>T</sub>幅と高さの (通常、両方とも 8)、transform ブロックには。
6. ドメイン空間残存情報を追加、[動き補償予測](motion-compensated-prediction.md)nonintra ブロック、または、アクセラレータ上で画像の再構築を実行する間ブロックの定数参照の値にします。 内のブロックの定数参照の値は 2<sup>(BPP 1)</sup>する場合を除く HostResidDiff (の 10 ビット、 **wMBtype**のメンバー、 [ **DXVA\_MBctrl\_P\_HostResidDiff\_1**](https://msdn.microsoft.com/library/windows/hardware/ff563993)) 構造体が 1 と**bConfigIntraResidUnsigned**のメンバー、 [ **DXVA\_ConfigPictureDecode** ](https://msdn.microsoft.com/library/windows/hardware/ff563133)構造体は 1 です。 後者の場合、定数には 0 です。

7. 0 ~ から画像の再構築したものを範囲にクリップ (2<sup>BPP</sup>)-1 とストアでの最終的な結果として得られる画像は、アクセラレータ上で値をサンプリングします。

 

 





