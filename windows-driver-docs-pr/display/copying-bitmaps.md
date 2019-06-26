---
title: ビットマップのコピー
description: ビットマップのコピー
ms.assetid: 76e07c66-7e57-42d7-b6da-c13c8e9a8dee
keywords:
- ビットマップ、GDI WDK Windows 2000 の表示
- ビットマップ グラフィックス ドライバー WDK Windows 2000 の表示
- WDK GDI、ビットマップの描画
- WDK GDI ビットマップ
- ビットマップのコピー
- DrvBitBlt
- DrvCopyBits
- DrvStretchBlt
- DrvTransparentBlt
- Windows 2000 の WDK の表示を拡大
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e41697888c75adcdf15c00d7ed39f9f09a178873
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370265"
---
# <a name="copying-bitmaps"></a>ビットマップのコピー


## <span id="ddk_copying_bitmaps_gg"></span><span id="DDK_COPYING_BITMAPS_GG"></span>


**ビット ブロック転送**(BitBlt) 関数の 1 つの画面からのビットのドライバー コピー ブロックによって実装されます。 これらの関数は次のとおりです。

[**DrvBitBlt**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvbitblt)

[**DrvCopyBits**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcopybits)

[**DrvStretchBlt**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstretchblt)

[**DrvTransparentBlt**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtransparentblt)

という名前のディスプレイ ドライバー固有 BitBlt 関数もあります[ **DrvSaveScreenBits**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsavescreenbits)します。

表面描画されている場合、*画面のデバイスで管理された*またはビットマップ、ドライバーは、ビット ブロック転送関数の最小レベルをサポートする必要があります。 標準の形式を GDI で管理されたビットマップを画面には、GDI は、ドライバーで接続されていない操作のみを処理します。

### <a name="span-iddrvbitbltspanspan-iddrvbitbltspan-drvbitblt"></a><span id="drvbitblt"></span><span id="DRVBITBLT"></span> DrvBitBlt

[ **DrvBitBlt** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvbitblt)関数は、一般的なビット ブロック転送機能を提供します。 ソースが使用されている場合**DrvBitBlt**先の四角形の上に元の四角形の内容をコピーします。 (、 *PptlSrc*この関数のパラメーターは、四角形の左上隅を識別します)。元の四角形が存在しない場合**DrvBitBlt**無視、 *pptlSrc*パラメーター。 先の四角形を変更する画面が 2 つの整数のポイント、左上で定義されているし、右下します。 四角形が*下の適切な排他的*; 四角形の右下隅は、ブロックの転送の一部ではないです。 **DrvBitBlt**空の送信先を示す四角形に呼び出すことはできません。 四角形の 2 つのポイントの順序が常に適切です。つまり、両方の右下の点の座標は、左上の点で、対応するよりも大きいです。

[**DrvBitBlt** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvbitblt)異なる Rop について説明し、デバイスによって最適化を実行します。 場合によっては、ROP が純色である場合、bitblt 関数ではなく、塗りつぶしを実行できます。 デバイスまたは Pscript ドライバーなど、Rop をサポートしていないドライバーの場合がありますの相違点表示および印刷されるイメージの間。

ブロック転送を処理する必要に応じて、 [ **DrvBitBlt** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvbitblt)マスクできる、インデックス変換色にはが含まれます。 色パレットのインデックスの変換を平行移動ベクターを支援します。 転送は、一連のクリップ四角形を使用して、ディスプレイ ドライバーによって任意にクリップされる必要があります。 GDI では、必要なリージョンと情報が割り当てられます。

実装する**DrvBitBlt**します。 Windows Driver Kit (WDK) で提供されている Microsoft VGA ドライバーでは、平面のデバイスの基本的な機能をサポートするサンプル コードを提供します。 実装する**DrvBitBlt**の他のデバイスがあまり複雑な可能性があります。

### <a name="span-iddrvcopybitsspanspan-iddrvcopybitsspan-drvcopybits"></a><span id="drvcopybits"></span><span id="DRVCOPYBITS"></span> DrvCopyBits

[ **DrvCopyBits** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcopybits) GDI 標準形式のビットマップのデバイスで管理されたラスター サーフェスとの間で変換するには、そのシミュレーション操作からの GDI によって関数が呼び出されます。 **DrvCopyBits** SRCCOPY (0xCCCC) ROP ビット ブロック転送を高速なパスを提供します。

ビットマップのデバイス管理とサーフェスのラスター グラフィックス ドライバーに必要なこの関数は、ドライバー サーフェスとの間の任意の標準形式のビットマップに変換する必要があります。 [**DrvCopyBits** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcopybits)空の送信先を示す四角形が呼び出されないと、先の四角形の 2 つのポイントの順序が常に適切です。 この呼び出しは、同じ要件[ **DrvBitBlt**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvbitblt)します。

ドライバーは、デバイス管理の画面またはビットマップをサポートする場合、ドライバーを実装する必要があります、 [ **DrvCopyBits** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcopybits)関数。 少なくとも、ドライバーは、次を実行する必要がありますと**DrvCopyBits**が呼び出されます。

-   デバイスの希望の形式とデバイスの画面には、ブロックの転送と、ビットマップの間を実行します。

-   SRCCOPY (0xCCCC) で転送を実行*ラスター オペレーション (ROP)* します。

-   任意のクリッピングを使用できます。

ドライバーは、GDI を使用できます[ **CLIPOBJ** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_clipobj)一連のクリップ四角形の領域を削減するサービスを列挙します。 GDI 渡します、平行移動ベクター、 [ **XLATEOBJ** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_xlateobj)色インデックスの変換元とコピー先の画面間を支援するために、構造体。

デバイスの画面は標準形式として整理*デバイスに依存しないビットマップ (DIB)* ドライバーは、単純な転送のみをサポートできます。 ドライバーがブロックの転送要求を後回しへの呼び出しで GDI に戻る場合は、複雑な ROP では、呼び出し、 [ **EngCopyBits** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcopybits)関数。 これにより、GDI をドライバーが実行できる簡単な関数呼び出しに分割します。

[**DrvCopyBits** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcopybits) RLE ビットマップが (Microsoft Windows SDK のドキュメントを参照してください) とも呼ばれますが、**デバイス依存ビットマップ (Ddb)** します。 ビットマップは、いくつかの Win32 GDI ルーチン アプリケーション プログラム呼び出しの結果としてこの関数に提供されます。 省略可能な DDB は、いくつかの特別なドライバーでのみサポートされます。

### <a name="span-iddrvstretchbltspanspan-iddrvstretchbltspan-drvstretchblt"></a><span id="drvstretchblt"></span><span id="DRVSTRETCHBLT"></span> DrvStretchBlt

必要に応じて、ドライバーを指定できます、 [ **DrvStretchBlt** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstretchblt)サーフェスのデバイス管理をサポートするドライバーであっても、機能します。 この関数は、デバイスに管理され、GDI で管理されたサーフェス間ブロック転送を拡大するための機能を提供します。 **DrvStretchBlt**伸縮、整数によって伸縮するなどの特定の種類のみをサポートしています。 倍数。

[**DrvStretchBlt** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstretchblt)ドライバー、ドライバーは、ハーフトーンを実行できる場合は特に、GDI ビットマップを記述することができます。 関数には、GDI ビットマップとデバイスの表面に適用される同じハーフトーン アルゴリズムも許可されます。

[**DrvStretchBlt** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstretchblt)ジオメトリック変換先の四角形に正確に幾何学的ソース四角形をマップします。 ソースが四角形の角のによって転置 (-0.5、-0.5 になります) 指定された整数の座標から。 関数のパラメーターで指定されたポイントは、ピクセルの中心に対応する整数の座標上に存在します。 このような 2 つのポイントで定義された四角形は、幾何学で、2 つの頂点の座標は特定のポイントからそれぞれ減算 0.5 を調整すると見なされます。 (GDI [ **POINTL** ](https://docs.microsoft.com/windows/desktop/api/windef/ns-windef-_pointl)構造体がこれら小数の座標の頂点を指定するため、短縮表記を使用します)。このような四角形の端がありません、ピクセルと交差が、ピクセルの一連の回ることに注意してください。 四角形内のピクセルは、下の右排他的な四角形の通常のピクセルです。

元の四角形の角に丸みを定義するポイントが適切に順序付けられた;[ **DrvStretchBlt** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstretchblt)空のソースの四角形を指定することはできません。 異なり[ **DrvBitBlt**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvbitblt)、 **DrvStretchBlt**出力のクリップで丸めエラーを防ぐための 1 つのクリッピング四角形を呼び出すことができます。

先の四角形は、整数の 2 つの点によって定義されます。 これらのポイントはも順序付けされません、2 番目の点の座標は、必ずしも、最初のよりも大きくしないことを意味します。 これらの点について説明するソース四角形では、右下隅は含まれません。 四角形が適切に順序付けされていないため、 [ **DrvStretchBlt** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstretchblt) x 座標または 2 つの y 座標の 2 つの場合がありますの逆転を実行する必要があります。 (ドライバーしようとしないで、ソースのサーフェイスに配置されていないピクセルを読み取る)。 **DrvStretchBlt**空の送信先を示す四角形に呼び出すことはできません。

色の翻訳の[ **DrvStretchBlt** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstretchblt) 、ポインターを提供*pxlo*を[ **XLATEOBJ** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_xlateobj)構造は、ソースと宛先表面の間で変換するために使用します。 XLATEOBJ 構造の任意のソース インデックス、コピー先インデックスを検索するクエリを実行できます。 高品質の伸縮ブロックの転送の**DrvStretchBlt**場合によっては色の補間するが必要です。 **DrvStretchBlt** COLORADJUSTMENT 構造体を使用しても、bits を拡大する前に、元のビットマップに適用される色の調整値を定義します。

[**DrvStretchBlt** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstretchblt)を使用して、 *i モード*ソース ピクセルの出力を組み合わせる方法を定義するパラメーター。 具体的には、 *i モード*出力画面で、出力の色または灰色のレベルを概算するピクセルのグループを使用するドライバーを許可するハーフトーン オプションを提供します。 COLORADJUSTMENT 構造体への変更は、次のドライバーに渡される**DrvStretchBlt**を呼び出し、 *i モード*ハーフトーンの。 さらに、ドライバーでは、GDI ハーフトーン GDI ビットマップを処理する必要がある場合、ドライバー フックを**DrvStretchBlt**、設定、 *i モード*ハーフトーン、パラメーターで返します[ **EngStretchBlt**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engstretchblt)します。

場合[ **DrvStretchBlt** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstretchblt)への呼び出しがフック、 [ **EngStretchBlt** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engstretchblt)関数し、は、サポートしない処理を行うように求められます、適切な関数で処理できるように、GDI に要求を返します。

### <a name="span-iddrvtransparentbltspanspan-iddrvtransparentbltspan-drvtransparentblt"></a><span id="drvtransparentblt"></span><span id="DRVTRANSPARENTBLT"></span> DrvTransparentBlt

[ **DrvTransparentBlt** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtransparentblt)関数により、コピーした後、移行先のビットマップの部分が表示されたままにできるように、コピー先ビットマップにコピーするソース ビットマップ。 *ITransColor*この関数のパラメーターを透明にするのには、色を指定します。

次の図は、透過的な blt の例を示しています。

![透過的な blt を示す図](images/transblt.png)

左から右に、上記の図は、元のビットマップ、透明の blt する前に、コピー先ビットマップとコピー先ビットマップを透過 blt 後に表示されます。 注意のカラー *iTransColor*上記 4 つのリージョンで、次に、およびソース ビットマップの中央の領域のいずれかの側と同じです。

Blt 操作が発生したとき、これら 4 つのリージョンはコピーされません、これにより、これらのリージョンを表示する コピー先のビットマップのピクセル パターン。 他の領域 (4 つの角およびセンター) の下の任意のピクセル パターンは、透過的な blt で上書きされます。

右端の画像に示す: 文字の部分は ' 4 つの角およびセンターで、元のビットマップの色で上書きされました。 文字の部分は ' 色では 4 つのリージョンではいるのと同じ*iTransColor*表示されたままにします。

 

 





