---
title: 4 2 の 2 ピクセルのビデオ形式
description: 4 2 の 2 ピクセルのビデオ形式
ms.assetid: 7064c7bd-bc7d-4b71-8876-ccb3a5808e45
keywords:
- 非圧縮ビデオ ピクセル形式の WDK DirectX VA
- 非圧縮ビデオ WDK DirectX VA のピクセル形式
- WDK の DirectX va なので、非圧縮ビデオのピクセル形式をデコードする圧縮の画像
- デコード WDK DirectX va なので、圧縮の画像します。
- 4 2 2 ビデオ WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0919efd2985e1c6dbb449267ce32f39943036c54
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387027"
---
# <a name="422-video-pixel-formats"></a>4:2:2 ビデオ ピクセル形式


## <span id="ddk_4_2_2_video_pixel_formats_gg"></span><span id="DDK_4_2_2_VIDEO_PIXEL_FORMATS_GG"></span>


圧縮された 4 をデコードする: 2:2 ビデオ、1 つの使用、次の圧縮されていないピクセル形式。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ピクセル形式</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>YUY2</p></td>
<td align="left"><p>データは、最初のバイトに Y の最初のサンプルが含まれている符号なし文字の配列としてメモリに存在、2 番目のバイトが Cb の最初のサンプルが含まれています、3 番目のバイトが Y の 2 つ目のサンプルが含まれています、4 番目のバイトには、Cr; の最初のサンプルが含まれています。などなど。 リトル エンディアン WORD 型の 2 つの変数の配列としてデータが処理されると、最初の単語は、最上位のビットで最下位ビットと Cb Y₀ を含むし、2 番目の WORD では、最下位ビットと Cr Y₁ を含む最上位ビットにします。 YUY2 が優先される DirectX VA 4:2:2 ピクセル形式。</p></td>
</tr>
<tr class="even">
<td align="left"><p>UYVY</p></td>
<td align="left"><p>YUY2、各単語のバイト順のスワップを除くと同じです。 リトル エンディアン WORD 型の 2 つの変数の配列としてデータが処理されると、最初の単語は、最上位のビットで最下位ビットと Y₀ Cb を含むし、2 番目の WORD では、最下位ビットと Y₁ Cr を含む最上位ビットにします。</p></td>
</tr>
</tbody>
</table>

 

 

 





