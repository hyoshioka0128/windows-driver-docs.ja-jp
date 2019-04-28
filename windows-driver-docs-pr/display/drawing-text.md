---
title: テキストの描画
description: テキストの描画
ms.assetid: e5bf4673-93c4-4cc5-b74d-e0e3a487ec3d
keywords:
- GDI WDK Windows 2000 の表示、テキスト出力
- グラフィックス ドライバー WDK Windows 2000 の表示、テキスト出力
- テキスト出力 WDK グラフィック
- DrvTextOut
- DrvGetGlyphMode
- 画面のテキスト出力 WDK GDI
- GDI WDK Windows 2000 の表示、テキスト、出力の描画
- グラフィック ドライバー WDK Windows 2000 の表示、描画、テキスト出力
- WDK GDI 描画のテキスト
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac8d72b24cbda278234b7520b8aefac9f9d04807
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377678"
---
# <a name="drawing-text"></a>テキストの描画


## <span id="ddk_drawing_text_gg"></span><span id="DDK_DRAWING_TEXT_GG"></span>


のみのテキストの出力関数を呼び出す、*画面のデバイスで管理された*(をデバイスにビットマップまたは画面) またはドライバーでの呼び出しがフックされている場合は、GDI で管理されたサーフェイスでの[ **EngAssociateSurface**](https://msdn.microsoft.com/library/windows/hardware/ff564183)関数。 テキストのグラフィック出力プリミティブは、関数です。

[**DrvTextOut**](https://msdn.microsoft.com/library/windows/hardware/ff557277)

[**DrvGetGlyphMode**](https://msdn.microsoft.com/library/windows/hardware/ff556230)

GDI 呼び出し**DrvTextOut**一連のテキスト出力の指定した位置にあるグリフのピクセルをレンダリングします。 多くは、 **DrvTextOut** GCAPS ビット機能を定義、 [ **DEVINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff552835)によって返される構造体、 [ **DrvEnablePDEV** ](https://msdn.microsoft.com/library/windows/hardware/ff556211)関数。

入力パラメーター **DrvTextOut** (ピクセル単位) の 2 つのセットを定義*フォア グラウンド*と*不透明*します。 ドライバーは、次の結果を提供する画面を表示します。

1.  不透明なピクセルには、最初に、不透明ブラシで表示されます。

2.  フォア グラウンド ピクセルは、前景ブラシを使用して、表示されます。

これらの各描画操作で実行、*クリップ領域*します。 クリップ領域の外側のピクセルの影響を受けることはできません。

不透明なピクセルが計算され、最初は不透明ブラシで、画面で描画されたために、ドライバーは、サーフェイスを描画する必要があります。 フォア グラウンドのピクセルが計算され、前景ブラシで描画されます。 これらの各操作は、クリッピングによって制限されます。

前景色と不透明なピクセルは、使用される色は、画面上につや消しマスクを構成します。 フォントのグリフ必要はありません、自体の色。 ピクセルのフォア グラウンド セットは、グリフのピクセルと取り消し線または下線をシミュレートするために使用される余分な特定四角形のピクセルの和集合として定義されます。 不透明なピクセルは、不透明な四角形によって定義されます。

**DrvTextOut**ポインター、pfo を使用して、現在のクエリに指定したフォントを選択します。 [ **FONTOBJ** ](https://msdn.microsoft.com/library/windows/hardware/ff565974)構造体。 このプロセスは、ソフト フォントまたはフォントの置き換えまたはデバイスに必要なフォント最適化のダウンロードを含めることができます。

呼び出す必要がありますが、ドライバーにスケーラブルなフォントがある場合、 [ **FONTOBJ\_pxoGetXform** ](https://msdn.microsoft.com/library/windows/hardware/ff566008)に現在 FONTOBJ 構造が、関連付けられているフォントをデバイスに概念的な変換を返す関数. これは、機能は、ドライバーによって提供されるフォントに必要です。 概念的な領域は、デバイス フォントのデザイン領域です。 たとえば、PostScript フォントは、1000 から 1000 でユニット文字セルで定義されます。 返されるメトリックのほとんどの[ **IFIMETRICS** ](https://msdn.microsoft.com/library/windows/hardware/ff567418)構造体は、デバイス概念的な変換が必要な理由は、概念的なスペースに変換されます。

グラフィックス エンジンでは、ドライバーをクエリ関数を呼び出すことによって[ **DrvGetGlyphMode** ](https://msdn.microsoft.com/library/windows/hardware/ff556230)のフォント情報をキャッシュには内部的にする方法を確認します。 ビットマップ、アウトライン、またはどちらも (に適した選択肢デバイス フォント) として個々 のグリフをキャッシュすることができます。

 

 





