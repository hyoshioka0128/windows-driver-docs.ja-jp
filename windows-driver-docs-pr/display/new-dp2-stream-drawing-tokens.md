---
title: 新しい DP2 ストリーム描画トークン
description: 新しい DP2 ストリーム描画トークン
ms.assetid: 09f3e5a4-60ed-4649-a30b-de4b320a54de
keywords:
- DirectX 8.0 リリース ノートには、Windows 2000 の WDK 表示 DP2 描画トークン
- DP2 描画トークン WDK DirectX 8.0
- 描画トークン WDK DirectX 8.0
- トークンの WDK DirectX 8.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 79321adf0c18f6dafbc7fc7a252502bfe9fe32bf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345541"
---
# <a name="new-dp2-stream-drawing-tokens"></a>新しい DP2 ストリーム描画トークン


## <span id="ddk_new_dp2_stream_drawing_tokens_gg"></span><span id="DDK_NEW_DP2_STREAM_DRAWING_TOKENS_GG"></span>


複数の頂点のデータ ストリームの DirectX 8.0 のサポートは、新しい DP2 描画トークンが導入されることが必要です。 既存の図面トークンは、特定の描画命令の頂点のデータを 1 つのポインターがあったことと見なされますためこれらの新しいトークンが必要です。 複数ストリームは、これは、不要になった場合。 描画コマンドがも複数の頂点データ バッファーに同時にアクセス ストリーム間で。

既存プリミティブを交換してトークンを描画してこれらの注意を入力して特定のトークン (たとえば、D3DDP2OP\_ポイント、D3DDP2OP\_TRIANGLELIST、D3DDP2OP\_TRIANGLESTRIP) 新しい DirectX 8.0 を通じて呼び出しインターフェイスのみです。 DX7 または以前のインターフェイスを通じて行われた呼び出しはまだ古いスタイルの描画トークンとして DDI を介して渡されます。 したがって、DX8 ドライバーはトークンを描画、新旧両方のスタイルをサポートするために必要です。

インデックスとインデックスなしの描画トークンでは、2 つのバリエーションがあります。 たとえば、インデックスなしの描画は、トークン D3DDP2OP で実現\_DRAWPRIMITIVE と D3DDP2OP\_DRAWPRIMITIVE2 します。 同様に、インデックス付きの描画は、トークン D3DDP2OP で実現\_DRAWINDEXEDPRIMITIVE と D3DDP2OP\_DRAWINDEXEDPRIMITIVE2 します。

2 つのバリエーションの主な違いは、その D3DDP2OP\_DRAWPRIMITIVE2 と D3DDP2OP\_DRAWINDEXEDPRIMITIVE2 は頂点データは、ランタイムによって変換されたときに使用されます。 これはか、ドライバーとハードウェアの組み合わせがハードウェア頂点処理をサポートしていないか、頂点を処理するソフトウェアがあるため明示的に選択されています。 これらのトークンのストリーム 0 のみが使用され、変換および照射の頂点が含まれています。

D3DDP2OP\_DRAWPRIMITIVE と D3DDP2OP\_DRAWINDEXEDPRIMITIVE は、ランタイムが頂点データを処理し、使用されます。 したがって、これらのトークンは、アプリケーションは、ランタイムに直接変換後のデータを指定するとハードウェアの頂点の処理または変換された頂点データをハードウェアがサポートする場合、未変換頂点データを指定できます。 この場合、ストリームの任意の数 (最大**MaxStreams**) アクティブにすることができます。 これらのバリアント (その他の新しい図面、トークンと共に D3DDP2OP\_CLIPPEDTRIANGLEFAN)、ランタイム内の最適なコード パスを有効にして、ここで説明するもの以外の違いは、ドライバーに重要ではありません。

 

 





