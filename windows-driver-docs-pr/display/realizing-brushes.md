---
title: ブラシの実現
description: ブラシの実現
ms.assetid: e6a7c008-50b2-4411-b8f8-99a3ca99e9f4
keywords:
- GDI WDK Windows 2000 の表示、パターン
- グラフィックス ドライバー WDK Windows 2000 の表示、パターン
- WDK GDI のパターン
- WDK GDI ブラシします。
- ブラシの原点 WDK GDI
- ブラシ WDK GDI の実現
- ディザー WDK Windows 2000 の表示
- ディザリング WDK Windows 2000 の表示の色
- WDK GDI の色の管理
- DrvRealizeBrush
- DrvDitherColor
- パターン WDK GDI のサーフェス ブラシ
- WDK GDI の塗りつぶし
- WDK GDI の行
- WDK GDI を描画ブラシします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 58708feb5e26ecd67154d88b0abf114e40bb4992
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351452"
---
# <a name="realizing-brushes"></a>ブラシの実現


## <span id="ddk_realizing_brushes_gg"></span><span id="DDK_REALIZING_BRUSHES_GG"></span>


線、テキストまたは塗りつぶしを出力するグラフィックス関数は、引数として少なくとも 1 つのブラシを受け取ります。 ブラシは、指定した画面で、グラフィックス オブジェクトを描画するために使用するパターンを定義します。 ブラシを受け取る関数に必要な各出力を*ブラシの原点*します。 ブラシの原点は、ブラシのパターンの左上のピクセルと連携して、デバイス画面上のピクセルの座標を提供します。 ブラシ パターンが、デバイス全体のサーフェイスをカバーする (並べて表示) で繰り返されます。

ドライバーは、ブラシを定義するには、次の関数をサポートできます。

[**DrvRealizeBrush**](https://msdn.microsoft.com/library/windows/hardware/ff556273)

[**DrvDitherColor**](https://msdn.microsoft.com/library/windows/hardware/ff556202)

ブラシは常に、既にデバイス画面上のデータとパターンを混在させる方法を定義する混在モードで使用します。 ミックスのデータ型は、1 つの ULONG 値にパックされている 2 つの ROP2 値で構成されます。 フォア グラウンド*ROP*最下位バイトが。 次のバイトには、バック グラウンド ROP が含まれています。 詳細については、Microsoft Windows SDK のドキュメントを参照してください。

GDI を使用するため、アプリケーションが要求したすべての論理ブラシの追跡を保持します。 何かを描画するためのドライバーを要求する前に GDI 最初の問題、ドライバー関数への呼び出し[ **DrvRealizeBrush**](https://msdn.microsoft.com/library/windows/hardware/ff556273)します。 これにより、独自の描画コードの必要なパターンの最適な表現を計算するドライバーができます。

*DrvRealizeBrush*によって定義されているブラシを実現するために呼び出される*psoPattern* (ブラシのパターン) および*psoTarget* (実現されたブラシの画面)。 実現されたブラシには、ドライバーは、パターンを使って領域を塗りつぶすが必要な情報およびアクセラレータが含まれています。 この情報が定義され、ドライバーでのみ使用します。 ブラシのドライバーの実現が記述された関数をサービスには、ドライバーは、GDI を呼び出すことによって割り当てられる可能性があるバッファーに[ **BRUSHOBJ\_pvAllocRbrush** ](https://msdn.microsoft.com/library/windows/hardware/ff538263)から内*DrvRealizeBrush*します。 GDI キャッシュすべて実現されたブラシ。その結果、再計算する、必要なことはほとんどありません。

*DrvRealizeBrush*、 **BRUSHOBJ**、または標準形式のビットマップ。 ラスター デバイスの場合は、ブラシ パターンを説明する画面はビットマップ; を表します。ベクターのデバイスでは、これは常にによって返されるパターン サーフェスのいずれかと、 [ **DrvEnablePDEV** ](https://msdn.microsoft.com/library/windows/hardware/ff556211)関数。 ブラシのために使用する透過マスクは、パターンと同じ程度にピクセルあたり 1 ビット ビットマップです。 マスク ビットの場合は、ピクセルが; ブラシの背景のピクセルにすると見なされることを意味します。つまり、ターゲットのピクセルは、その特定のパターンのピクセルによる影響はありません。 *DrvRealizeBrush*を使用して、 [ **XLATEOBJ** ](https://msdn.microsoft.com/library/windows/hardware/ff570634)デバイスのカラー インデックスにブラシ パターンでの色を変換する構造体。

ドライバーは、サービスの GDI 関数を呼び出す必要があります[ **BRUSHOBJ\_pvGetRbrush** ](https://msdn.microsoft.com/library/windows/hardware/ff538264)ときの値、 **iSolidColor** BRUSHOBJ 構造体のメンバーは、0 xffffffff と**pvRbrush**メンバーが**NULL**します。 **BRUSHOBJ\_pvGetRbrush**指定ブラシのドライバーの実現へのポインターを取得します。 GDI を自動的に呼び出す場合は、ドライバーは、この関数を呼び出すときに、ブラシが満たされていない、 *DrvRealizeBrush*ブラシのドライバーの実現にします。

### <a name="span-idditheringspanspan-idditheringspanspan-idditheringspandithering"></a><span id="Dithering"></span><span id="dithering"></span><span id="DITHERING"></span>ディザリング

必要に応じて、GDI は、ハードウェアを正確に表すことができない単色のブラシを作成しようとするときに、ドライバーのアシスタンスを要求できます。 GDI は、ドライバー関数を呼び出す**DrvDitherColor**します。

選択された色を概算するいくつかの色のパターンを使用してディザリングと、その結果、デバイスのカラー インデックスの配列。 これらの色、パターンを使って作成されたブラシは、通常は、指定された色の十分な概算です。 [**DrvDitherColor** ](https://msdn.microsoft.com/library/windows/hardware/ff556202)デバイスによって正確に指定することはできませんの色を表すこともできます。 これを行う*DrvDitherColor*いくつかの色のパターンを要求し、特定の純色を近似するブラシを作成します。

関数は、 *DrvDitherColor*は省略可能であり、場合にのみ呼び出されます、GCAPS\_色\_ディザーまたは GCAPS\_MONO\_ディザー機能フラグが設定されて、 **flGraphicsCaps**のメンバー、 [ **DEVINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff552835)構造体。 *DrvDitherColor*次の表に記載した値を返すことができます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">値</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DCR_DRIVER</p></td>
<td align="left"><p>ディザー値が、ドライバーによって計算されていることを示します。 識別するハンドルを<strong>cxDither</strong>によって<strong>cyDither</strong>このケースで戻されたデバイスのカラー インデックスの配列。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DCR_HALFTONE</p></td>
<td align="left"><p>GDI が既存のデバイス (ハーフトーン) パレットを使用して色を概算する必要がありますを示します。 たとえば、GDI では、のみ 3 または 4 つの色を含む、プリンターの一般的なパレットを使用することができます。 DCR_HALFTONE は、デバイスには、VGA 16 アダプター カードは、標準固定パレットなどのデバイス (ハーフトーン) パレットが含まれている場合にのみ、ディスプレイ ドライバーで使用できます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DCR_SOLID</p></td>
<td align="left"><p>GDI が (多対一) 既存のデバイス パレットで色の最も近い値に要求された色をマップすることを示します。</p></td>
</tr>
</tbody>
</table>

 

モノクロのドライバーをサポートする必要があります*DrvDitherColor* GDI 灰色レベルの優れたパターンを取得するためにします。

 

 





