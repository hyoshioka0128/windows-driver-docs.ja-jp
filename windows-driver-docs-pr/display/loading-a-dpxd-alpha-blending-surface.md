---
title: DPXD アルファ ブレンドの読み込み画面
description: DPXD アルファ ブレンドの読み込み画面
ms.assetid: 6b5f62e9-3211-42c2-8168-505983c7814e
keywords:
- stride WDK DirectX VA
- データ読み込みの WDK DirectX VA をアルファ ブレンド
- ブレンド画像 WDK DirectX va なので、アルファ ブレンドのデータの読み込み
- DPXD アルファ ブレンド画面 WDK DirectX VA
- デコードの PXD アルファ ブレンド画面 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec64f0474d7248694225aa08466d6ca8ab5d0f44
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556470"
---
# <a name="loading-a-dpxd-alpha-blending-surface"></a>DPXD アルファ ブレンドの読み込み画面


## <span id="ddk_loading_a_dpxd_alpha_blending_surface_gg"></span><span id="DDK_LOADING_A_DPXD_ALPHA_BLENDING_SURFACE_GG"></span>


デコードされた PXD (DPXD) アルファ ブレンド画面は、フレームのバイト配列として定義されます。 フレーム データの各バイトには、2 ビットの 4 つのサンプルが含まれています。 各 2 ビットのサンプルは、(表示コントロール コマンド) のデータの強調表示し、DCCMD によって決定される 4 色のテーブルにインデックスに使用されます。 DPXD、強調表示、および DCCMD の組み合わせの結果は IA44 サーフェスに相当し、描画の 16 エントリ YUV パレットと共に使用します。 次の例は、次の 2 ビット DPXD アルファ ブレンド画面を処理するは、バイト、最初の 2 ビット サンプルのインデックスの配列が DPXD データの最初のバイトの最上位ビットであるため場合、は、3 番目のサンプルは、次の 2 ビットで、、4 番目のサンプルは、最下位ビットには、5 番目のサンプルは、次のバイト、という具合の最上位ビットにします。

DVD に関する PXD 情報から、DPXD アルファ ブレンドの画面を作成できます。 (PXD データは、実行の長さでエンコードされた形式での DVD に記録されます)。DVD に PXD から DPXD の作成には、実行の長さが DVD の生の PXD データのデコードを実行するホスト デコーダーが必要です。

画面の stride は、ストライド (バイト単位)、2 ビットのサンプルではなくとして解釈する必要があります。 ただし、幅と高さは、サンプルの 2 ビット単位で指定する必要があります。

**注**   PXD、DVD にはフィールド構造のインター レース形式。 DirectX VA に対して定義されている DPXD アルファ ブレンドの画面にはありません。 DVD PXD データから DPXD を形成する場合は、2 つのフィールドからのデータをインタリーブのホストは、そのためです。

 

DVD サブピクチャ定義およびデータ フィールドの解釈の詳細については、次を参照してください。*読み取り専用のディスク、DVD 仕様。パート 3 - ビデオ Specification (version 1.11、1999 年 5 月)* します。

 

 





