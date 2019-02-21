---
title: PCL XL GPD ファイルへの書き込み
description: PCL XL GPD ファイルへの書き込み
ms.assetid: 35abc33a-a046-452b-b650-5c4f626bf6cb
keywords:
- PCL XL ベクター グラフィックス WDK Unidrv、GPD ファイルの書き込み
- GPD ファイル WDK Unidrv、PCL XL
- WDK PCL XL の順序コマンド
- PCL XL GPD ファイルの書き込み
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b89db1789728e3d220193fd5247cdd6ceddd67a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527713"
---
# <a name="writing-a-pcl-xl-gpd-file"></a>PCL XL GPD ファイルへの書き込み





PCL XL GPD ファイルで有効にする方法と PCL XL ストリーム内の PCL XL コマンドの順序がどのファイルなど、GPD ファイルが含める必要があります、このセクションでは、PCL XL GPD ファイルの書き込みに関する一般的な情報を提供します。

Windows Driver Kit (WDK) でサンプル PCL XL GPD ファイル (p6sample.gpd) を含む、 \\src\\印刷\\ミニ\\mdw\\ベクター\\pcl6 ディレクトリ。 (このリソースできない場合がありますのいくつかの言語および国。)

### <a name="files-to-include"></a>含めるファイル

GPD ベース ミニドライバーを作成するには、プリプロセッサ ディレクティブを使用して\*GPD の次のファイルを指定します。

pclxl.gpd--を読み、理解しやすい GPD コードを記述するように、PCL XL 演算子のマクロが含まれます。 たとえば、記述することができます =**BeginPage**の代わりに&lt;43&gt;します。

p6disp.gpd--pcl5eres.dll と pclxl.dll に含まれるリソース文字列のマクロが含まれます。

p6font.gpd--pclxl.dll に含まれているフォントのマクロが含まれます。

pjl.gpd--PJL コマンドのマクロが含まれています。

上記のファイルだけでなく standard GPD ファイル、stdnames.gpd および ttfsub.gpd が含まれます。

次の例では、GPD ファイルでこれらのファイルを含めると方法を示します。

```cpp
*Include: stdnames.gpd
*Include: ttfsub.gpd
*Include: pclxl.gpd
*Include: p6disp.gpd
*Include: p6font.gpd
*Include: pjl.gpd
```

### <a name="enabling-pcl-xl-support-in-the-gpd-file"></a>PCL XL GPD ファイル サポートを有効にします。

PCL XL ベクターのサポートを有効にするには、のみを設定する必要が、\*パーソナリティ属性。 これは、次のように行います。

```cpp
*Personality: = PERSONALITY_PCLXL
```

パーソナリティ\_stdnames.gpd で PCLXL 定数が定義されています。

サンプル GPD ファイル、p6sample.gpd、新しい PCL XL ミニドライバーを作成する開発者向けに WDK に含まれます。

### <a name="pcl-xl-command-ordering"></a>PCL XL コマンドの順序付け

コマンドの順序は、PCL 5 よりも PCL XL にさらに重要です。 PCL ストリーム内の小さなエラーは、ジョブに影響する可能性はありませんが、PCL XL コマンドは、PCL XL (PCL 6) ですべてのエラーが原因で、XL のエラー ページに生成されるため、ストリーム内の特定のポイントでのみ有効です。 たとえば、BeginSession 演算子を送信する前に BeginPage 演算子を送信することはできません。

PCL XL ストリームでは、次のような形式があります。 (に示すインデントは、これらの演算子は、ペアになって、ポイントを強調するためにのみ使用されます)。

```cpp
PJL commands
BeginSession
  OpenDataSource
    BeginPage
      <page data>
    EndPage
  CloseDataSource
EndSession
PJL commands
```

PCL XL ストリームは、前にその後に PJL コマンド。 PCL XL ストリーム自体が、BeginSession 演算子で始まり EndSession 演算子で終了します。 演算子のペア、内では、もう 1 組の演算子があります。OpenDataSource および CloseDataSource します。 内で 1 つまたは複数の BeginPage/EndPage 演算子の組み合わせ、1 つのペアをプリンターに送信される各ページには演算子の組み合わせ。 など、個々 のページを表示する方法を説明するページ データが、BeginPage/EndPage 演算子のペアで囲まれた部分します。

PCL XL のすべての演算子の詳細についてを参照してください、 *PCL XL 機能参照プロトコル クラス 2.0*ドキュメント。

### <a name="additional-information-about-pcl-xl-gpd-files"></a>PCL XL GPD ファイルに関する追加情報

PCL XL GPD ファイルで、 \*FontFormat 属性名は、フォントをダウンロードする方法を指定するは 2 つの値に制限されます。HPPCL\_アウトラインと HPPCL\_RES します。 最初の値は、Unidrv が TrueType アウトライン データをダウンロードすることを示します。 2 番目の値は、Unidrv がビットマップ ソフト フォント データをダウンロードすることを示します。

IHV をダウンロードするには、フォントの数を制限することで、または指定されたフォントでは、ダウンロードする文字数を制限することでプリンターのメモリ使用量を減らすことができます。 \*MinFontID と\*MaxFontID 属性の名前を使用すると、これらの値で指定された範囲内にある Id を持つソフト フォントをダウンロードする Unidrv に通知します。 同様に、 \*MinGlyphID と\*MaxGlyphID 属性の名前を使用すると、特定の範囲内にダウンロードする指定されたフォントのグリフの数を制限します。

Unidrv は、独自のディザー マトリクスには各 GPD ファイルが含まれているという前提で動作します。 また、独自のディザー マトリクスを各デバイスがあることをお勧めします。 ディザー マトリクスがで指定された、\*機能。ディザー[カスタマイズされた機能](customized-features.md)します。

 

 




