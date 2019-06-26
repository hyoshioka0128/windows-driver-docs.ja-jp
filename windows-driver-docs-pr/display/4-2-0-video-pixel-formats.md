---
title: 4 2 0 ビデオのピクセル形式
description: 4 2 0 ビデオのピクセル形式
ms.assetid: fb83336b-ff71-4f54-b833-324da60e7f9e
keywords:
- 非圧縮ビデオ ピクセル形式の WDK DirectX VA
- 非圧縮ビデオ WDK DirectX VA のピクセル形式
- WDK の DirectX va なので、非圧縮ビデオのピクセル形式をデコードする圧縮の画像
- デコード WDK DirectX va なので、圧縮の画像します。
- 4 2 0 ビデオの WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ff6831ff4fdba483c4d811096068c4be140aa72
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384272"
---
# <a name="420-video-pixel-formats"></a>4:2:0 ビデオ ピクセル形式


## <span id="ddk_4_2_0_video_pixel_formats_gg"></span><span id="DDK_4_2_0_VIDEO_PIXEL_FORMATS_GG"></span>


圧縮された 4 をデコードする: 2:0 ビデオ、1 つの使用、次の圧縮されていないピクセル形式。

| **ピクセル形式** | **説明** | 
|:--|:--|
| YUY2 | 」の説明に従って[4:2:2 ビデオ ピクセル形式](vscode-resource://c:/drivers/drivers/windows-driver-docs-pr/display/4-2-2-video-pixel-formats.md)出力 Cb の 2 つの行と Cr サンプルが 4 の実際の行はごとに生成されることを除いて、: 2:0 Cb および Cr のサンプルです。 出力行の各ペアの 2 行目では、通常、いずれかと重複している最初の行のまたはペアの最初の行で、[次へ] のペアの最初の行のサンプルのサンプルの平均を計算によって生成されます。 | 
| UYVY | 」の説明に従って[4:2:2 ビデオ ピクセル形式](vscode-resource://c:/drivers/drivers/windows-driver-docs-pr/display/4-2-2-video-pixel-formats.md)出力 Cb の 2 つの行と Cr サンプルが 4 の実際の行はごとに生成されることを除いて、: 2:0 Cb および Cr のサンプルです。 出力行の各ペアの 2 行目では、通常、いずれかと重複している最初の行のまたはペアの最初の行で、[次へ] のペアの最初の行のサンプルのサンプルの平均を計算によって生成されます。 | 
| YV12 | すべての Y サンプルの直後に (の半分のストライド、Y の行と行の数を半分)、すべての Cr サンプル (場合によっては、大きい stride のメモリのアラインメントの) での符号なし文字の配列としてメモリ内で最初に見つかった、直後にすべて Cb同様の方法でのサンプルです。 | 
| IYUV | Cb および Cr 平面の順序を入れ替えるを除き、YV12 と同じです。 | 
| NV12 | どのすべての y サンプル、最初に見つかったメモリ内 (場合によってはメモリのアラインメントの大きい stride) での行の数が偶数の符号なしの char 型の配列として書式設定します。 これは、直後にインターリーブ Cb、Cr のサンプルを含む符号なしの char 型の配列。 これらのサンプルは、リトル エンディアン WORD 型としてアドレス指定、Cb は最下位ビットになり、Cr の Y サンプルと同じ合計ストライドを持つ最上位ビットになります。 NV12 が優先される 4:2:0 ピクセル形式。 | 
| NV21 | 符号なしの char 型の値の彩度の配列になります (とになるよう場合は、リトル エンディアン WORD 型としてアドレス指定、Cr の最下位ビットになります Cb よう最大限記号になります。 各サンプルについては、Cb を続けて Cr ようにをスワップするサンプルの Cb および Cr を除く、NV12 と同じificant ビットの場合)。 | 
| IMC1 | YV12 と同じ点を除いて Cb、Cr のストライド平面が Y 平面に stride と同じです。 また、Cb、Cr の平面はする必要があります行 16 の倍数であるメモリ境界に分類されます。 次のコード例は、Cb の計算を表示し、Cr の平面します。<br/>`BYTE* pCr = pY + (((Height + 15) & ~15) * Stride);`<br/>`BYTE* pCb = pY + (((((Height * 3) / 2) + 15) & ~15) * Stride);`<br/>上記の例では、pY はメモリの配列の先頭を指すバイト ポインターと高さは 16 の倍数である必要があります。 | 
| IMC2 | 半 stride の境界でその Cb、Cr の行を除く、IMC1 と同じではインターリーブされます。 つまり、クロミナンス領域の全 stride の各行は、Cr、続く次の半分 stride 境界から開始 Cb の行の行を開始します。 (これは IMC1 よりもよりアドレス-領域を効率よく形式、半分にクロミナンス アドレス空間を切り取り、アドレス空間の合計が 25% 行え、ため)。これは NV12、関連のオプションで希望の形式ですが、人気のある NV12 が表示されます。 | 
| IMC3 | Cb と Cr スワップすることを除き、IMC1 と同じです。 | 
| IMC4 | Cb と Cr スワップすることを除き、IMC2 と同じです。 | 

これらの形式の詳細については、次を参照してください。[ビデオをレンダリングするための推奨の 8 ビット YUV 形式](https://docs.microsoft.com/windows/desktop/medfound/recommended-8-bit-yuv-formats-for-video-rendering)Microsoft メディア ファンデーション ドキュメント。
