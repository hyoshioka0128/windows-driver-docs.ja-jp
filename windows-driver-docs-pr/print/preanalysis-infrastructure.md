---
title: 事前分析インフラストラクチャ
description: 事前分析インフラストラクチャ
ms.assetid: 4c07145a-9a08-4507-8bab-769617e73d77
keywords:
- バンディング WDK Unidrv
- 事前分析インフラストラクチャ WDK Unidrv
- ブラックバンド WDK Unidrv
- DrvStretchBlt
- OEMStretchBlt
- DrvStartBanding
- DrvNextBand
- DrvQueryPerBandInfo
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0cd1e981498d9871dac83c4a6bacc4846e661044
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844661"
---
# <a name="preanalysis-infrastructure"></a>事前分析インフラストラクチャ





事前分析インフラストラクチャは、Unidrv が印刷ジョブのバンドを強制的に適用し、各ページの最初のバンド再生がページ全体を含むバンドであるようにするメカニズムです。 事前分析パスはレンダリングを許可せず、オブジェクトがレンダリングされる前にページ上のオブジェクトの分析を有効にするためだけに実行されます。

フルページ事前分析を可能にするために、Unidrv は最初に[**DrvEnableSurface**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablesurface)関数内の全ページのデバイス画面を指定し、次に、最初のバンドが[*DrvQueryPerBandInfo*](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvqueryperbandinfo)によってページ全体のサイズであることを示します。 事前分析が完了した後、Unidrv は*DrvQueryPerBandInfo*を使用して、事前分析が有効になる前にクリッピング領域をそのサイズに戻します。その後、Unidrv はそのサーフェイスにレンダリングします。 GDI の実装の制限により、事前分析は、N アップモードが 1\_の場合、またはレンダリングバンドがページ全体の場合にのみ有効にすることができます。

次の擬似コードは、事前分析に使用されるロジックを示しています。

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

事前分析機能は、現在の汎用プリンターの説明 (GPD) ファイルとプラグインで動作する必要があるため、テキスト z オーダー、空のバンド検出、およびその他の操作は、ミニドライバーの観点からは非表示で実装されます。 ミニドライバーは[**DrvStartBanding**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstartbanding)と[**DrvNextBand**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvnextband)をフックできますが、 **DrvNextBand**の最初の呼び出しにレンダリングが含まれていないため、 **DrvNextBand**への最初の呼び出しは受信されません。 このプラグインは、OEM オブジェクトレベルの事前分析を可能にする GPD でフラグを設定した場合にのみ、最初の**DrvNextBand**呼び出しを受信します (\***PreAnalysisOptions**: 8)。 この場合、プラグインは**DrvStartBanding**と**DrvNextBand**をフックする必要があり、プラグインは**DrvStartBanding**関数の*pptl*パラメーターをチェックする必要があります。 *Pptl*パラメーターが**NULL**以外の場合、事前分析は無効になります。 *Pptl*パラメーターが**NULL**の場合、事前分析パスの開始を示します。 この場合、プラグインは、DDIs を描画するためのすべての呼び出しで、プラグインが事前分析パスからの結果をフックしたものと見なします。 事前分析パスは、 **DrvNextBand**関数の最初の呼び出しで終了し、 **DrvNextBand**関数の最初の呼び出しの後に描画パスが開始されます。 この関数の後続の呼び出しには、レンダリングデータが含まれます。

### <a href="" id="-preanalysisoptions-modes"></a>PreAnalysisOptions モードの\*

事前分析モードは、GPD ファイルで、\***PreAnalysisOptions**: *n*属性名と属性パラメーターによって制御されます。 次の表に、\***PreAnalysisOptions**属性名と共に使用できるパラメーター値の一覧を示します。 これらの値のうち2つ以上を組み合わせて、複数のオプションを有効にすることができます。

パラメーターの意味値0

すべての事前分析モードを無効にします。

1

既定のモード。 モノクロの z オーダーテキスト分析と空白帯域幅の最適化を有効にします。 このモードは、ダウンロード可能なフォントまたはデバイスのフォントサポートと高解像度 (600 dpi 以上)、24 BPP レンダリングモードのデバイスに対して有効です。

2

24 BPP [**Iprintoemuni:: ImageProcessing**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing)コールバックに対して 1 BPP の最適化を有効にします。

ホーム フォルダーが置かれているコンピューターにアクセスできない

デバイスの StretchBlt 操作を有効にします。

8

OEM オブジェクトレベルの事前分析を有効にします。

 

### <a name="monochrome-z-order-text-analysis-with-blank-band-optimization"></a>空の帯域幅最適化を使用したモノクロの Z オーダーテキスト分析

```cpp
*PreAnalysisOptions: 1
```

\***PreAnalysisOptions**パラメーターを1に設定すると、Unidrv は次の操作を実行できます。

-   モノクロプリンターのテキストオブジェクトとグラフィックオブジェクトの間の z オーダーで問題を検出します。

-   空の帯域幅の最適化を実行します。

最初の操作では、モノクロプリンターにダウンロードされたテキストが後で上書きされるか、またはグラフィックスオブジェクトと対話するときに発生する z オーダーの問題を処理します。 Z オーダーの問題は、多くの場合、複雑なクリップを含むグラフィックオブジェクトによって発生します。これにより、Unidrv は、以前にダウンロードされたテキストをクリアする白い四角形をダウンロードできなくなります。

Unidrv は、レンダリングパスを実行する前に、各ページで事前分析パスを実行します。 Unidrv は、シミュレートできない複雑なクリップを使用するビットブロック転送 (blt) オブジェクトと共にテキストが重なっているかどうかを判断します。 このため、テキストは直接ダウンロードされるのではなく、サーフェイスビットマップにレンダリングされるので、後でレンダリングされるオブジェクトはテキストを正しく操作できます。

さらに、白い四角形をサポートしていないデバイスの場合、Unidrv は複雑なクリップを含まない場合でも、blts によってオーバーレイされるテキストをチェックします。 Unidrv は、プリンターに直接ダウンロードするのではなく、テキストをサーフェイスにレンダリングします。

次の描画コマンドは、後続の blts によってオーバーレイされる可能性のあるテキストに対してテストされます。

-   [**DrvBitBlt**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvbitblt)

-   [**DrvStretchBlt**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstretchblt)

-   [**DrvStretchBltROP**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstretchbltrop)

-   [**DrvStrokeAndFillPath**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokeandfillpath)

したがって、このモードでは、テキスト領域オブジェクトと塗りつぶされた領域オブジェクトのすべての z オーダーの問題を修正する必要があります。 テキストとオーバーレイ線に問題が残っている可能性があることに注意してください。 このようなソリューションでは、すべてのテキストが描画されるのではなく、ほぼすべてのテキストがダウンロードされる可能性があるため、これらの状況は含まれていません。

この機能では、デバイスフォントの使用に関連する z オーダーの問題は修正されません。 アプリケーションまたはドライバーがデバイスのフォントモードを選択している場合、ドライバーはこの問題を修正することができず、デバイスのフォントを画面に表示できません。

2番目の操作では、Unidrv がページ上の空白領域を最適化できるようにします。 このモードでは、空の上余白と下余白、およびページの中央にある大きな空白の領域に対して、Unidrv がスキップされます。 このモードは、カラー印刷で使用するためのものであり、ページをレンダリングするために必要な帯域幅の数を最小限に抑えることでパフォーマンスを向上させます。

事前分析パスの実行中に、Unidrv は、ページ上で描画が発生する場所を決定します。 空のバンドの最適化は、事前分析が有効になっている場合、またはプリンターが高解像度 (600 dpi 以上) で 24 BPP レンダリングバンドを使用している場合に有効になります。これにより、インクジェットプリンター用の 24 BPP レンダリングのパフォーマンスが著しく向上し、既存の OEM プラグインを変更する必要がなくなります。

### <a name="black-band-optimization"></a>黒の帯域幅の最適化

```cpp
*PreAnalysisOptions: 2  *% 1 bpp ImageProcessing bitmaps
```

\***PreAnalysisOptions**パラメーターを2に設定すると、Unidrv はより大きな 1 bpp の縞模様を使用して、純色の黒のオブジェクトのみを含む領域をレンダリングできます。これは、ページ全体を 24 BPP でレンダリングすることではありません。 このモードは空白バンドの最適化に似ていますが、ページ上の塗りつぶされた黒い領域 (カラー領域ではなく) も決定されます。 1 bpp の縞模様で表示できるのは、黒色 (灰色の網掛けなし) のオブジェクトだけです。 24 BPP の色に設定されたハーフトーンは、1 BPP のモノクロでは正しくレンダリングされないためです。

Unidrv は、 [**DrvEnableSurface**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablesurface)関数内に2つのサーフェイスを作成します。1つは色、もう1つは 1 BPP モノクロです。 Unidrv では、それぞれに同じメモリを使用するため、追加のメモリは必要ありません。 ページ preanalysis は、ページに単色の黒または空白の領域が含まれているかどうかを判断します。これは、色を含む領域の場合よりも大きなバンドを使用できます。 カラー領域では、より小さいカラーバンド画面を使用する必要があります。

同じメモリ量を使用している場合、1 BPP のモノクロサーフェイスは 24 BPP のカラーサーフェイスとして24倍のサイズになります。 したがって、ページの中央にある色だけを含むイメージは、上部の領域、色を含む領域、および下部の領域に分割できます。 この3つの領域は、次のようにして設定できます。最上部の領域は1つのモノクロのバンドに配置できます。色を含む領域は、その領域をカバーするために必要な数のカラーバンドに分割できます。また、下の領域は1つのモノクロのバンドに配置できます。

この機能を利用するには、Oem が**Iprintoemuni:: ImageProcessing**コールバックをサポートし、ラスターデータのダンプを処理する必要があります。 **Iprintoemuni:: ImageProcessing**コールバックの現在の OEM プラグインサポートは、24 BPP バンドまたは 1 BPP ソリッドの黒いバンドを受け入れるように拡張する必要があります。

### <a name="support-for-device-stretchblt-operations"></a>デバイスの StretchBlt 操作のサポート

```cpp
*PreAnalysisOptions: 4
```

\***PreAnalysisOptions**パラメーターを4に設定すると、Unidrv は、stretchblt 操作をサポートするデバイスに[**DrvStretchBlt**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstretchblt)呼び出しを直接ダウンロードできます。

Unidrv が 24 BPP カラーデータを生成する場合、すべての stretchblt イメージがデバイスの解像度に拡張されるため、大量のラスターデータをダウンロードする必要があります。 これにより、多くの東アジアプリンターのメモリ不足の状態に加えて、パフォーマンスが低下する可能性があります。

ミニドライバー render プラグインは、 [**Oemstretchblt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printoem/nf-printoem-oemstretchblt)をフックして独自のイメージダウンロードコマンドを提供する必要があるため、stretchblt モードを利用するために必要です。 Unidrv は、直接ダウンロードできる呼び出しでのみ OEMStretchBlt フックを許可します。 そのため、このプラグインは、z オーダーの問題の処理には関与しません。 このプラグインでは、受け取った OEMStretchBlt 呼び出しに含まれるソースイメージデータを直接ダウンロードすることのみが必要です。 このプラグインでは、イメージがプラグインでサポートされていない形式またはダウンロードできない形式である場合に、イメージを Unidrv に戻すオプションもあります。

オブジェクトがデバイスに直接ダウンロードされ、他のデータがシステムにレンダリングされるたびに、z オーダーの問題やハーフトーンの不整合が発生する可能性があります。 このモードでは、事前分析を使用して、直接ダウンロードできる stretchblts を決定します。 直接ダウンロードする場合は、マスクまたは複雑なクリッピングを含まない stretchblts だけが考慮されます。 ダイレクトダウンロードの対象となっている stretchblts のいずれかを後のオブジェクトがオーバーレイする場合、オブジェクトは直接ダウンロードされません。 この原則により、パフォーマンスが向上し、システムとデバイスの両方にハーフトーンが含まれているイメージがないことを確認する必要があります。これにより、品質の低い印刷出力が生成されます。

### <a name="oem-object-level-preanalysis-hooks"></a>OEM オブジェクトレベルの事前分析フック

```cpp
*PreAnalysisOptions: 8
```

\***PreAnalysisOptions**パラメーターを8に設定すると、OEM は事前分析パスを開始できます。これにより、ページ全体のすべてのオブジェクトが、帯域幅に関係なく[**DrvStartBanding**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstartbanding)呼び出しの後に再生されるようになります。 Preanalysis パス中は Unidrv 内に描画は許可されませんが、Oem はすべての DrvXxx drawing 呼び出しをフックして、ページ上のオブジェクトを分析することができます。

このモードの機能は、Oem がオブジェクトベースの色補正やレンダリングを使用できるように、カラーインクジェットプリンターに焦点を合わせています。 たとえば、一部のプリンターでは、黒のオブジェクトが色オブジェクトと交差している場合に、そのオブジェクトを個別に処理する必要があります。 他の Oem では、bitblt オブジェクトとは異なる、stretchblt オブジェクトのハーフトーンが必要になる場合があります。 Stretchblt オブジェクトは、Windows がサポートする任意のグラフィックスファイル形式 (.png や .jpg など) にすることができます。 Bitblt オブジェクトは、排他的なビットマップです。

GPD でこのモードが有効になっている場合、Unidrv は画面を縞模様として定義しますが、最初の再生はページ全体で行われます。 これを行うために、Unidrv は GDI クリップウィンドウをページ全体に設定します。 Unidrv を使用すると、すべての描画コマンドをフックできますが、描画を実行する前にを返します。 次のパスでは、Unidrv はクリップウィンドウを通常のバンドサイズにリセットし、通常どおりバンドに戻します。

Oem は、GPD でこのモードを有効にしたときに、 **DrvStartBanding**と[**DrvNextBand**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvnextband)の両方をフックする必要があります。 **DrvStartBanding**関数の*pptl*パラメーターをテストして、Unidrv が指定されたページでこのモードで事前分析を有効にできるかどうかを判断する必要があります。 *Pptl*パラメーターが**NULL**の場合、Unidrv で事前分析が有効になっています。 Unidrv はこの時点では意味がないため (バンド位置では更新されていないため)、 *pptl*パラメーターを使用します。 事前分析の場合、バンド位置は常に (0, 0) に設定されます。 *Pptl*パラメーターが**NULL**の場合、OEM は最初の**DrvNextBand**の前のすべての描画呼び出しを事前分析の一部として考慮する必要があり、サーフェイス上に描画されないようにする必要があります。

事前分析の終了は、 **Oemnextband**関数の呼び出しによって通知されます。 **Oemnextband**に渡される*Pptl*パラメーターが**NULL**ではありません。 この呼び出しは、適切な*pptl*値を Unidrv に返すためにのみ使用されます。 プラグインでは、 *pptl*値を自分で設定することも、Unidrv にコールバックすることもできます (このトピックの冒頭にある前の擬似コード例のように)。 **Oemnextband**の最初の呼び出しで指定された**oemnextband**の*pso*パラメーターがまだ表示されていないため、バンドサーフェスはデバイスにコンテンツを送信しません。

 

 




