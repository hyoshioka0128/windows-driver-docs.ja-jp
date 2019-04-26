---
title: フレーム バッファー構造
description: フレーム バッファー構造
ms.assetid: 2a9ce844-84c5-4517-acf7-c7e67a1e5e07
keywords:
- DirectX のビデオ アクセラレータ WDK Windows 2000 の表示、ビデオのデコード
- ビデオ アクセラレータの WDK DirectX のビデオのデコード
- VA WDK DirectX、ビデオのデコード
- ビデオの WDK DirectX va なので、フレーム バッファーの組織のデコード
- ビデオのデコード WDK DirectX va なので、フレーム バッファー組織
- フレーム バッファー組織 WDK DirectX VA
- WDK DirectX VA をバッファー処理します。
- 予測は、WDK DirectX VA をブロックします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: efe643a2130d6cb64058d4af53ca520b15130996
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348297"
---
# <a name="frame-buffer-organization"></a>フレーム バッファー構造


## <span id="ddk_frame_buffer_organization_gg"></span><span id="DDK_FRAME_BUFFER_ORGANIZATION_GG"></span>


すべてのバッファーを画像は、mpeg-2 ビデオ仕様 (サンプルの場所は、フレームの座標として示されます) で説明するようフレーム編成バッファーと見なされます。

損失のない予測のブロックを変換する、実装に固有の変換レイヤーを使用することは (を参照してください*非可逆圧縮*) フレームの座標フィールド座標に記載されています。 たとえば、モーション予測を 1 つのフレームは上位 2 つの個別に分けることが、マクロ ブロック部分の予測を下します。

3 つのビデオ コンポーネント チャネル (Y, Cb, Cr) は、DirectX 問い合わせください。 に対して定義されているインターフェイスを使用してデコードします。 2 つのクロミナンス コンポーネント (Cb、Cr) の動きベクトルは、輝度コンポーネント (Y) に送信されたものから取得されます。 アクセラレータは、これらの動きベクトルのいずれかに変換するために使用できるさまざまな座標システム。

次の図は、ビデオ データ バッファリングは、ホストとアクセラレータで実装します。

![ビデオ データがホストとアクセラレータのシステムにバッファリングするかを示す図](images/hostaccsys.png)

 

 





