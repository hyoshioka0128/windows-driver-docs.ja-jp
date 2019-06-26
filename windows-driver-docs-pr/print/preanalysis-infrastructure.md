---
title: 事前分析インフラストラクチャ
description: 事前分析インフラストラクチャ
ms.assetid: 4c07145a-9a08-4507-8bab-769617e73d77
keywords:
- バンドの WDK Unidrv
- preanalysis インフラストラクチャ WDK Unidrv
- 黒い帯 WDK Unidrv
- DrvStretchBlt
- OEMStretchBlt
- DrvStartBanding
- DrvNextBand
- DrvQueryPerBandInfo
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f0064a37baaaf7c7f57cfa0cd68677eb6afc13d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373798"
---
# <a name="preanalysis-infrastructure"></a>事前分析インフラストラクチャ





Preanalysis インフラストラクチャは、各ページの最初のバンドの再生がバンド全体のページが含まれているように、印刷ジョブの縞模様を Unidrv が強制するメカニズムです。 Preanalysis パスは、レンダリングを許可しないと、オブジェクトがレンダリングされる前に、ページ上のオブジェクトの分析を有効にする場合にのみ実行されます。

ページ全体の preanalysis できるように、Unidrv 最初を指定します内でページ全体のデバイスの画面、 [ **DrvEnableSurface** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablesurface)関数とし、最初のバンドの方法でページ全体のサイズであることを示します[ *DrvQueryPerBandInfo*](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvqueryperbandinfo)します。 Preanalysis 後が完了すると、Unidrv 使用*DrvQueryPerBandInfo* preanalysis が有効にします前に、そのサイズに戻す、クリッピング領域を復元するには。Unidrv を後でその画面に表示します。 N-up モードである場合にのみ GDI の実装の制限事項、ため preanalysis を有効にできます\_UP、またはページ全体がレンダリング バンド。

次の疑似コードは、preanalysis のためのロジックを示しています。

```cpp
DrvEnableSurface
if( preanalysis enabled )
   Use dummy device surface
DrvStartDoc
For each physical page 
{
   DrvStartPage
   DrvStartBanding
   For each banding surface 
   {
      DrvQueryPerBandInfo
// Set sizlBand member of PERBANDINFO
      if( preanalysis_pass ) 
         pbi.sizlBand = {whole page}
      else 
         pbi.sizlBand = {normal band}
      Carry out rendering operations
      if ( ( preanalysis pass && OEM preanalysis enabled ) || !preanalysis_pass ) {
         Call OEM hooks
         DrvNextBand
      }
      if ( ( preanalysis pass && OEM preanalysis enabled ) || !preanalysis_pass )
         Call OEMNextBand
      if( preanalysis pass ) {
         Disable preanalysis
         Switch from dummy device surface to real device surface
      }
      if( last band ) 
         Write end page character from GPD
   }  // for each banding surface

}  // for each physical page
DrvEndDoc
```

Preanalysis 機能は、現在のジェネリックのプリンターの説明 (GPD) を使用する必要がありますので、ファイルとプラグイン、テキストの z オーダー、空白のバンドの検出、およびその他の操作が実装されなかった見えない、ミニドライバーの観点から。 フックできる、ミニドライバー [ **DrvStartBanding** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstartbanding)と[ **DrvNextBand**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvnextband)、最初の呼び出しを受け取ることはありませんが、 **DrvNextBand**ため、最初の呼び出しは**DrvNextBand**レンダリングには含まれません。 最初の受信、プラグイン**DrvNextBand** OEM オブジェクト レベル preanalysis できる GPD でフラグに設定する場合にのみ呼び出します (\***PreAnalysisOptions**:8). ここで、プラグインする必要がありますをフック**DrvStartBanding**と**DrvNextBand**、プラグインを確認する必要があります、 *pptl*のパラメーター、 **DrvStartBanding**関数。 場合、 *pptl*パラメーターは非**NULL**preanalysis が無効になっています。 場合、 *pptl*パラメーターが**NULL**、preanalysis パスの先頭を示します。 この場合、プラグインを想定してください preanalysis パスから結果をすべてのプラグインがフック Ddi の描画呼び出し。 Preanalysis パスは、最初の呼び出しで終わる、 **DrvNextBand**関数、およびレンダリング パスの開始を最初に呼び出した後、 **DrvNextBand**関数。 この関数への後続の呼び出しは、レンダリング データが格納されます。

### <a href="" id="-preanalysisoptions-modes"></a>\*PreAnalysisOptions モード

Preanalysis モードによって GPD ファイル内で制御する、 \* **PreAnalysisOptions**: *n*属性の名前と属性のパラメーター。 次の表で使用できるパラメーター値、 \* **PreAnalysisOptions**属性の名前。 複数のオプションを有効にするのには、これらの値の 2 つ以上を結合できます。

パラメーターの意味値 0

すべての preanalysis モードを無効にします。

1

既定モードです。 モノクロの z オーダーのテキストの分析と空白のバンドの最適化を有効にします。 ダウンロード可能なフォントまたはデバイス フォントのサポートと高解像度でデバイスをこのモードが有効になっている (600 dpi 以上)、24 BPP レンダリング モード。

2

24 ビット/ピクセルの 1 ビット/ピクセルの最適化を有効にする[ **IPrintOemUni::ImageProcessing** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing)コールバック。

4

デバイス StretchBlt 操作を有効にします。

8

OEM オブジェクト レベル preanalysis を有効にします。

 

### <a name="monochrome-z-order-text-analysis-with-blank-band-optimization"></a>空白のバンドの最適化を使用して、モノクロの Z オーダーのテキスト分析

```cpp
*PreAnalysisOptions: 1
```

設定、 \* **PreAnalysisOptions**パラメーターを 1 により、次の操作を実行する Unidrv:

-   Z オーダーのテキストとグラフィック オブジェクトのモノクロ プリンター間での問題を検出します。

-   空白のバンドの最適化を実行します。

最初の操作では、モノクロ プリンターにダウンロードされるテキストは、後で上書きされますまたはそれ以外の場合、グラフィックス オブジェクトと対話する際に発生する問題を z オーダーを処理します。 Z オーダーの問題が原因グラフィック オブジェクト Unidrv は以前ダウンロードしたテキストをクリアすること白い四角形をダウンロードすることができるように、複雑なクリップを含む多くの場合です。

Unidrv では、レンダリング パスを与えて前に、各ページに preanalysis パスが実行します。 Unidrv をシミュレートすることはできませんを複雑なクリップを使用するビット ブロック転送 (blt) オブジェクトで任意のテキストをオーバーレイ対象かどうかを判断します。 したがって、テキストは後で表示されるオブジェクトが、テキストと正しく対話を直接ダウンロードではなくサーフェスのビットマップにレンダリングされます。

さらに、白い四角形をサポートしていないデバイスの場合は、任意のテキストの複雑なクリップが含まれていない場合でも、blt によってオーバーレイ Unidrv を確認します。 Unidrv では、プリンターに直接ダウンロードするのではなく、画面上にテキストをレンダリングします。

次の描画コマンドは、後続 blt によってオーバーレイがテキストに対してテストされます。

-   [**DrvBitBlt**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvbitblt)

-   [**DrvStretchBlt**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstretchblt)

-   [**DrvStretchBltROP**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstretchbltrop)

-   [**DrvStrokeAndFillPath**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokeandfillpath)

そのため、このモードでは、テキスト入力領域オブジェクトの間のすべての z オーダーの問題を修正する必要があります。 まだ問題があるテキストと線をオーバーレイに注意してください。 このようなソリューションがほぼすべてのテキストが描画されているのではなくダウンロード中のため、このような状況は含まれません。

この機能では、デバイスのフォントの使用に関連する z オーダーの問題は修正されません。 アプリケーションまたはドライバーがデバイス フォントのモードを選択した場合、ドライバーはこの問題を解決することはできず、画面上にデバイス フォントを表示することはできません。

2 番目の操作には、ページ上の空白領域を最適化する Unidrv ができます。 このモードでは、空の上部と下部の余白、ページ中央の大規模な空白領域上 Unidrv がスキップされます。 このモードでは、カラー印刷で使用するためのものでは、ページを表示するために必要なバンド パスの数を最小限に抑えることでパフォーマンスを向上します。

Preanalysis のパスの間に、ページの描画が行われる Unidrv を決定します。 Preanalysis が有効になっている場合、またはプリンターが高解像度で 24 BPP レンダリング バンドを使用する場合、空白のバンドの最適化が有効になっている (600 dpi 以上)。これは、インク ジェット プリンターの 24 BPP レンダリングでは顕著なパフォーマンスの向上が生成されを既存の OEM プラグインの変更は必要ありません。

### <a name="black-band-optimization"></a>黒のバンドの最適化

```cpp
*PreAnalysisOptions: 2  *% 1 bpp ImageProcessing bitmaps
```

設定、 \* **PreAnalysisOptions**パラメーターを 2 には、Unidrv 大きい 1 BPP 24 ビット/ピクセルにページ全体を表示するのではなく、オブジェクトを含むのみ solid 黒、リージョンを表示するために画面を縞模様を使用します。 このモードは、空白のバンドの最適化をページ上の (色の領域) ではなく黒い領域を純をも決定例外に似ています。 黒一色 (灰色の濃淡がありません) であるだけのオブジェクトは、1 ビット/ピクセルの白黒のハーフトーン 24 ビット/ピクセルの色に設定が正しく表示されないため、画面を縞模様 1 のビット/ピクセルで表示できます。

Unidrv 内の 2 つのサーフェスを作成し、 [ **DrvEnableSurface** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablesurface)関数: 1 のビット/ピクセルの白黒の他の色を 1 つ。 Unidrv ごとに、同じメモリを使用して追加のメモリは必要ありません。 ページ preanalysis は、ページには拡大バンドできます使われるよりも色が含まれているリージョンのソリッド黒または空白領域が含まれて かどうかを判断します。 色のリージョンのみでは、小さい色バンド画面を使用して必要があります。

同量のメモリを使用するには、1 ビット/ピクセルの白黒画面は 24 ビット/ピクセルの色の画面の 24 時間の大きなできます。 ページの中央のみの色を含むイメージを分割して、3 つのリージョンにそのため、: 最上位のリージョンや、色を含む領域下の領域。 これら 3 つのリージョンは次のように縞模様ことができます。 上のリージョンは、モノクロのバンドを 1 つに配置できます、色が格納されているリージョンは、多くの色のバンドをカバーするために必要なように分けることが、および下の領域は、モノクロのバンドを 1 つに配置することができます。

この機能がサポートするために Oem が必要です、 **IPrintOemUni::ImageProcessing**コールバックをラスター データのダンプを処理します。 プラグインの現在の OEM のサポート、 **IPrintOemUni::ImageProcessing** 24 BPP バンドまたは 1 のビット/ピクセル solid 黒い帯のいずれかをそのまま使用するコールバックを強化する必要があります。

### <a name="support-for-device-stretchblt-operations"></a>デバイス StretchBlt 操作のサポート

```cpp
*PreAnalysisOptions: 4
```

設定、 \* **PreAnalysisOptions**パラメーターを 4 により、ダウンロードする Unidrv [ **DrvStretchBlt** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstretchblt)デバイスを直接呼び出してはそのサポート stretchblt操作です。

Unidrv では、24 ビット/ピクセル カラー データを生成するときは、stretchblt のすべてのイメージを拡大して非常に大量のラスター データをダウンロードする必要がありますデバイスの解像度します。 これは、結果、東アジア言語のプリンターの多くのメモリ不足の条件に加え、パフォーマンスの低下。

プラグイン ミニドライバー レンダリングがそれをフックする必要がありますので、stretchblt モードの利用に必要な[ **OEMStretchBlt** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printoem/nf-printoem-oemstretchblt)し、独自のイメージのダウンロード コマンドを指定します。 Unidrv では、直接ダウンロード可能な呼び出しでのみ OEMStretchBlt フックを使用できます。 したがって、プラグインはありませんを z オーダーの問題を処理します。 受信した OEMStretchBlt 呼び出しに含まれるソース イメージ データを直接ダウンロードのみにプラグインの必要があります。 プラグインは、イメージが、プラグインはサポートしていませんまたはダウンロードできない形式の場合、Unidrv にイメージを punting のオプションが。

オブジェクトは、システムの他のデータを表示中にデバイスにダウンロード直接、たびにあります z オーダーの問題またはハーフトーン不整合。 このモードでは、preanalysis を使用して、どの stretchblts を直接ダウンロードを調べます。 直接ダウンロードをマスクまたは複雑なクリッピングを含まない stretchblts のみが検討されます。 場合、後でオブジェクトのオーバーレイ、直接ダウンロードは後でないオブジェクトを検討している stretchblts のいずれかが直接ダウンロードされます。 この原則は、パフォーマンスが向上する必要があり、イメージが含まれているなし、両方のシステムと、デバイスは、非常に低品質の印刷出力の結果からハーフトーンにはことを確認する必要があります。

### <a name="oem-object-level-preanalysis-hooks"></a>OEM オブジェクト レベル Preanalysis フック

```cpp
*PreAnalysisOptions: 8
```

設定、 \* **PreAnalysisOptions** 8 へのパラメーターにより、後に再生がすべてのページ全体でオブジェクトように preanalysis パスを開始する OEM、 [ **DrvStartBanding**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstartbanding)バンドのサイズに関係なく呼び出します。 Preanalysis のパスの間に Unidrv 内で許可されている描画はありませんが、Oem は、すべての描画呼び出し、ページ上のオブジェクトを分析する DrvXxx をフックできます。

カラー インク ジェット プリンターにはこのモードで機能がフォーカスがある Oem がオブジェクトに基づく色補正やレンダリングに使用できるようにします。 たとえば、特定のプリンターでは、単独で表示される黒いオブジェクトではなく、色のオブジェクトと交差する場合は、黒のオブジェクトを異なる方法で処理する必要があります。 その他の Oem は、bitblt 関数オブジェクトとは異なる stretchblt オブジェクトのハーフトーンを必要があります。 Stretchblt オブジェクトは、.png または .jpg など、Windows をサポートする任意のグラフィック ファイル形式にできます。 Bitblt 関数オブジェクトは、ビットマップのみです。

このモードは、GPD で有効な場合、Unidrv は縞模様のサーフェイスとして、画面を定義しますが、によりページ全体の最初の再生。 これを行うには、Unidrv は GDI クリップのウィンドウをページ全体に設定します。 Unidrv により、すべての描画コマンドをフックするが、描画前に取得を実行することができます。 次のパスで Unidrv リセット クリップ ウィンドウ バンドと通常のバンドのサイズに通常どおりします。

Oem は両方をフックする必要があります**DrvStartBanding**と[ **DrvNextBand** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvnextband) GPD でこのモードを有効にするとします。 また、テストする必要があります、 *pptl*のパラメーター、 **DrvStartBanding** Unidrv preanalysis 指定ページには、このモードでを有効にすることができるかどうかを判断する関数。 場合、 *pptl*パラメーターが**NULL**Unidrv が preanalysis を有効にします。 Unidrv を使用して、 *pptl*パラメーター (これが更新されていないバンドの位置この時点では意味があるないため。 Preanalysis のバンドの位置は常に設定 (0, 0))。 場合、 *pptl*パラメーターが**NULL**、OEM は、1 つ目の前にすべての描画呼び出しを検討**DrvNextBand** preanalysis の一部であるとする必要がありますの描画を許可しませんサーフェイス。

呼び出しによって通知される preanalysis の末尾、 **OEMNextBand**関数。 *Pptl*パラメーターに渡される**OEMNextBand**ない**NULL**します。 この呼び出しは、適切なを返す場合にのみ使用*pptl* Unidrv する値。 プラグインを設定できる、 *pptl*自体を値またはにコールバックする Unidrv (など、このトピックの先頭の前の疑似コード例では、)。 画面の縞模様のため、 *pso*パラメーターの**OEMNextBand**最初の呼び出しで指定された**OEMNextBand**はレンダリングされません、プラグインを送信しないでください、デバイスにコンテンツ。

 

 




