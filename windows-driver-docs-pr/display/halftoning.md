---
title: ハーフトーン
description: ハーフトーン
ms.assetid: 94cf0d87-055d-470e-94ca-225d519aeb14
keywords:
- GDI WDK Windows 2000 の表示、ハーフトーン
- グラフィックス ドライバー WDK Windows 2000 の表示、ハーフトーン
- 描画の WDK GDI、ハーフトーン
- ハーフトーン WDK GDI
- 固定のセル間隔 WDK GDI
- WDK GDI ハーフトーン サイズ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb576f81cac73f922c31faccb087fed2c7c2834e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372956"
---
# <a name="halftoning"></a>ハーフトーン


## <span id="ddk_halftoning_gg"></span><span id="DDK_HALFTONING_GG"></span>


従来のアナログ ハーフトーン セルが固定の間隔を中心に、等しいサイズのセルから成るハーフトーン 画面を使用します。 セルが固定の間隔では、各セル内のドットのサイズは継続的なトーンの印象を生成するために異なる場合に、インクの太さが対応します。

コンピューターでは、ほとんどの印刷や画面の網かけは固定のセルのピクセル サイズも使用します。 変数のドットのサイズをシミュレートするには、クラスターのピクセルの組み合わせは、ハーフトーン画面をシミュレートします。 GDI には、十分な最初の概算を提供するハーフトーン既定のパラメーターが含まれています。 その他のデバイスに固有の情報は、出力を向上させるために、システムに追加できます。

ドライバー送信 GDI GDI を介してハーフトーンを行う必要があるデバイスの仕様、 [ **GDIINFO** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_gdiinfo)によって返される構造体、 [ **DrvEnablePDEV**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablepdev)関数。 ドライバーとパターンのサイズを指定します、 **ulHTPatternSize** GDIINFO、ハーフトーンの出力形式を定義するのメンバー。 特定のデバイスはハーフトーン ハーフトーン パターンのサイズに関するものです。 GDI は、2 x 2. ~ 16 x 16 からさまざまな定義済みのパターンのサイズを提供します。

それぞれの標準的なパターンのサイズの変更後のバージョンもあります。 サフィックスによって識別されます。"\_M"標準的なパターンのサイズの名前にします。 たとえば、標準の 6 ~ 6 をパターンに定義された名前は、HT\_PATSIZE\_6 x 6、変更後の 6 ~ 6 でパターンの名前は HT\_PATSIZE\_6 x 6\_M)。 変更後のバージョンでは、色の解像度が高いのできますが、水平または垂直のノイズの副作用を生成することができます。 さらに、これらのパターンのサイズのそれぞれは、デバイスの解像度に依存であるために、適切なパターンのサイズは、特定のデバイスに依存します。

パターン (空間の解決策) のサイズと色の解像度のトレードオフについては、パターンのサイズによって決まります。 大規模なハーフトーン パターンは、小さなパターンが最適な空間の解決に結果の中により良い色の解像度を生成します。 パターンに最適なサイズの決定は、頻繁に、試行錯誤の問題です。 詳細についてを参照してください[ **GDIINFO**](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_gdiinfo)します。

ハーフトーンに影響を与える GDIINFO 構造体メンバーのもう 1 つは**flHTFlags**ハーフトーンに必要なデバイスの解像度を示すフラグを含むです。

GDI ハンドルは、色のアプリケーションからの要求を調整し、グラフィックス DDI を使用してドライバー関数に情報を渡します。 アプリケーションは、ハーフトーンを選択し、画面は、標準形式*DIB*、その後、そのハーフトーン機能を使用してビットマップを処理する GDI ビットマップがデバイスに送信します。 PostScript ドライバーで、 [ **EngStretchBlt** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engstretchblt)関数は、いずれかを使用してプリンターにビットマップを送信できます、 [ **DrvCopyBits** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcopybits)または[ **DrvBitBlt** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvbitblt) (SRCCOPY モード) で機能します。

WYSIWYG 高画質で高速化の出力を提供、GDI PostScript プリンターではなくハーフトーンを実行できるようにすること、します。 PostScript ドライバーへのインターフェイスには、ハーフトーンを調整するユーザーができ、プリンターの組み込みのハーフトーン機能が推奨される場合、GDI ハーフトーンをオフにする チェック ボックスを提供します。

[ **DrvDitherColor** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdithercolor)関数は、DCR を返すことができます\_ハーフトーン値は、GDI が既存のデバイス (ハーフトーン) パレットを使用して色をおおよそを要求します。 DCR\_ハーフトーンで使用できる、ディスプレイ ドライバー、デバイスには、VGA 16 アダプター カードなどのデバイス (ハーフトーン) パレットが含まれている場合にのみ固定パレットの標準があるためです。 ほとんどのラスター プリンターを含む、モノクロのドライバーを使用できます、 *i モード*でパラメーター *DrvDitherColor*良いグレースケール効果を取得します。

**注**   Windows 2000 以降では、24 ビット (またはそれ以降) デバイスでは、ハーフトーンはできません。

 

 

 





