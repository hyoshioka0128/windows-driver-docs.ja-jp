---
title: 擬似ベクトル グラフィックス サポート
description: 擬似ベクトル グラフィックス サポート
ms.assetid: 8eeba51b-00fa-4bf3-a78c-ac1d1adc9696
keywords:
- ベクター グラフィックス WDK Unidrv、pseudovector グラフィック
- pseudovector グラフィックス WDK Unidrv
- nonvector グラフィックス デバイス WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 90582e540cba9e034bc1f818131871859c66c5b1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358461"
---
# <a name="pseudo-vector-graphics-support"></a>擬似ベクトル グラフィックス サポート





True のベクター グラフィックスをサポートしていないデバイスでは、pseudovector グラフィックスの Unidrv を提供するサポートを利用できます。 この機能を使用するときに Unidrv ダウンロード黒い実線の四角形と水平方向および垂直の線 nonvector グラフィックス デバイスに直接ラスター画面で、これらの図形をレンダリングするオーバーヘッドが縮小されます。 これは、ラスター データを効率的に処理しないデバイスのプリンターのスループットを向上させることができます、出力データのサイズも減少します。

この機能からメリットを得る、nonvector グラフィックス デバイスのミニドライバーは CmdRectBlackFill コマンドをサポートするためだけ必要があります。 この機能が無効になっているときに、**印刷の最適化**機能、 **[詳細設定]** プリンターのプロパティ ページのタブがになっています。

Pseudovector のグラフィックス機能への呼び出しをインターセプトする[ **DrvBitBlt**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvbitblt)、 [ **DrvStrokePath**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokepath)、および[ **DrvLineTo**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvlineto)が solid 黒の四角形または垂直方向または水平方向の線を描画するかどうかを決定します。 Unidrv (黒一色は、複雑なクリッピングを持たないおよび現在の変換先の bits を使用して ROP を使用しないもの) 有効な四角形として描画する図認識されると、表面に描画されているのではなく四角形配列に格納されます。

Pseudovector グラフィック機能のにおける最も難しい部分は、以前描画オブジェクトの上に描画する必要がありますオブジェクトによって発生 z オーダーの問題を回避するは。 上のオブジェクトが消去または黒の四角形の一部を上書きする必要があります。 場合は黒の四角形は、デバイスに既にダウンロードされているが、後で描画オブジェクト システム画面可能性がありますは描画されません正しく。

この問題の解決策では、一時的に画面ですぐに描画するのではなく、有効な四角形を格納します。 新しいオブジェクトは、画面上に描画されますが、オブジェクトがすべて黒の四角形と重複しているかどうかを確認する Unidrv を確認します。 場合は、黒の四角形の重複部分が表面に描画最初に、新しいオブジェクトが描画される、正確な z 順序維持したままにします。 四角形を描画最初も考慮可能性を描画する新しいオブジェクトはコピー先と連携する 1 つ以上のそれに関連付けられている ROP でいる可能性があります。

さらに、新しいオブジェクト描画するのににはは、結果として得られる図は、四角形が不要になったように複雑なクリッピングが含まれていることができます。 バンドやページ レンダリングが完了したら、残りの黒い長方形直接ダウンロードできますをデバイスに z オーダーの問題を発生させることがなく。 Unidrv では、可能であれば、BitBlt 四角形を連結バンド、あたり最大で 256 台の四角形の一覧を保持します。

### <a name="pseudovector-graphics-issues"></a>Pseudovector グラフィックスの問題

Pseudovector のグラフィックス機能変更される可能性が、z オーダー特定の状況で特にテキストがデバイスに直接ダウンロードされ、複雑なクリッピングの後続のオブジェクトは、そのテキストと対話する必要があります。

 

 




